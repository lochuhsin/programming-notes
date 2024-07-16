---
created: 2024-01-08 23:14
aliases:
  - validate jwt
tags: 
card link:
  - "[[JWT]]"
source:
---
## Description
---

The main concept is pretty easy. The relation states:  
`Signature = SomeHashFunc(Base64URL(Header)+Base64URL(Payload)+secret)`

As a client, we can get the header, the payload, and the signature. The crucial part is the secret. If we have the secret, we could easily validate the token.

In general, there are two scenarios to get the secret. 

1. First, the client will get the public key and cache it in the server. Whenever the JWT token comes, client could validate it.

	However, there are some downsides. The most significant one is that the public key is distributed across all severs. This violates the basic rule.

	What “Auth0” does is that, it exposes a specific API endpoint for clients to fetch data whenever the JWT token comes. The client only needs to maintain the URL endpoint in as a secret.

2. What if the client is not able to validate the token ? Then the client would need to send the token back to the issuer, who signed to send the JWT token, This is also a valid way.

	Unfortunately, this is extremely inefficient, to validate each JWT token in each request will cause huge performance loading to the issuer server.

	This is so-called *back-channel* communication between the client and the issuer.

## Reference
---

[How JWT works ?](<https://stackoverflow.com/questions/76548676/is-it-possible-to-validate-a-jwt-token-without-having-the-secret-key>)
