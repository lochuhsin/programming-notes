---
created: 2024-01-09 10:13
aliases: 
tags: []
card link:
  - "[[JWT]]"
source: https://stackoverflow.com/questions/76548676/is-it-possible-to-validate-a-jwt-token-without-having-the-secret-key
---
## Description
---

> Recently I’ve been learning about JWT. And I was planning to adopt JWT on Next.js server with an external auth server that issues JWT access token. At first I was thinking about this following logic (when fecthing data)

The saying “_When your only tool is a hammer…_” comes to mind.

(For clarity, I’ve tweaked your event-sequence by adding common terms from the OAuth/OIDC specs)

> 1. Client sends request with JWT access token (and waits for a response from RP).
> 2. some external server (the RP) receives that request
> 3. the RP sends the JWT access token to the auth server (IdP) that issued JWT token to validate
> 4. the RP rejects or accepts the client’s request based on the IdP’s response in step 3, and completes the client’s request from step 1.
> 
> But I thought this was very inefficient.

Correct, it is inefficient.

- What you’re describing there is _back-channel_ communication between the RP and the IdP.
	
	- Using the back-channel is not normally necessary because it defeats the purpose of using a distributed authX scheme in the first place (as it _requires_ the back-channel to be reliable, otherwise the RP can’t work, and overall it hinders RPs in the system from acting independently).
	- Normally all communication between the IdP, the client, and RPs is done via the “front-channel”, which is when the client is responsible for passing messages between the IdP and the RP (usually in the form of Cookies and Bearer tokens in HTTP requests).
- As a parenthetical: note that JWTs are not normally encrypted as none of the _claims_ within a JWT should themselves be “secret” values (but you [can encrypt JWTs](https://stackoverflow.com/questions/27301557/if-you-can-decode-jwt-how-are-they-secure) if you absolutely need to); also note that if you’re not the IdP then you have no control over this; also note that some schemes and systems may require JWTs to be unencrypted, but that’s another question).
	
- Some back-story on signatures in JWT:
	
	- The RP needs to be able to know it can trust the _claims_ in the JWT came from the IdP: this is ensured by having the IdP cryptographically signing the JWT and by ensuring the RP can verify that signature somehow.
		
	- The RP can then verify the signature by either:
		
		1. Already having the key required to run the signature verification algorithm locally.
		2. Delegating the verification back to the IdP.
	- In a well-functioning distributed system there should be minimal dependence between systems, so the second option (delegating verification to the IdP) is undesirable, so we should prefer the first option - and that first option _does not_ require the use of symmetric keys (which must be kept secret).
		

> Then I saw a blog post that says “_JWT is better than other token-based authentication solutions because it does not make further validation requests to auth server but a microservice itself validates a token’s validity_”

The truth is actually far more complicated: the article you read is an unfortunate example of someone mixing broad and specific terminology together and coming to an inaccurate (and incomplete) conclusion (especially with the implication that JWT is the _only_ scheme that supports distributed asymmetric-cryptographic signatures, because it isn’t).

> But isn’t it impossible to validate a JWT token without secret key? If so, is it safe to store a JWT secret key inside many different microservices? (I am using dotenv to store secret key)

No. You need to understand how asymmetric encryption works in this case; but first, remember that JWTs can be signed with _many different kinds_ of techniques, not just asymmetric cryptographic signatures.

For simplicity, follow this flowchart:

1. RP receives a non-encrypted, but signed JWT. The `iss` (Issuer, the IdP) and `aud` (Audience, the RP) claims in the JWT correctly correspond to the IdP and RP.
2. If the JWT is signed with an asymmetric algorithm (such as `RS256` or `ES256`) it means the JWT was signed with the IdP’s (secret) _private_ key, and the signature can be verified with the IdP’s _public key_ which the RP will need to be able to access.
	1. The RP _should_ already have the IdP’s public-key cached locally: if the RP receives a JWT signed with a key it doesn’t have the public-key for then **yes**: the RP will need to contact the IdP directly for it and cache it (this is defined by the overarching scheme, like OIDC, which requires the IdP to expose its public keys at `https://{authority}/.well-known/openid-configuration`).
	2. The RP then uses the IdP’s public-key to verify the signature on the JWT - and also validate the `nbf` (Not-Valid-Before) and `exp` (Expiry) claims, and any other minimally necessary claims.
		- Signature verification does not require any communication or involvement from the IdP, excepting retrieving the public key, which should only need to happen _once_, _ever_ (and to keep things simple, the act of retrieving the public-key can happen during RP’s server startup sequence or during system deployment/configuration (which is necessary for air-gapped networks, for example) so it never happens when the RP receives a JWT-based request.
3. If a JWT is signed with a symmetric (non-asymmetric) algorithm (such as `HS256`), then there’s two ways to continue:
	
	- (Note that symmetrically-signed JWTs are a bad idea: it allows the RP to create its own JWTs too, which means the IdP needs to trust the RP not to abuse its secret key, but rule #1 in distributed systems is _do not trust anyone_.)
	
	1. Option 1: both the IdP and the RP *_need_ to have the symmetric (secret) private key already in their local key cache. As with asymmetric keys, the RP can get this from the IdP on-demand via the _back-channel_, or it can be preshared and given to RP during the RP’s deployment or startup process.
	2. Option 2: If the RP cannot be trusted with a symmetric private secret key then the RP needs to make a back-channel request to the IdP that passes the entire JWT back to the IdP for verification (the IdP will respond with a simple “yes/no”: as the RP can still use the claims within the JWT as they aren’t encrypted).
		- The RP _can_ cache the IdP’s yes/no response (based on some unique characteristic of the JWT, such as its hash or token-id), of course, to avoid having to make a back-channel request to the IdP for _every_JWT-based request that client makes.


## Reference
---





