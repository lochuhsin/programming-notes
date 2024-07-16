---
created: 2024-01-08 22:38
aliases:
  - jwt token
  - jwt
tags: 
card link: 
source:
---
## Description
---

JWT is a commonly used Base64 encoded web token. There are three components.

- Header
- Payload
- Signature

Which is connected with dots like:  
`xxxxxxxx.yyyyyyyyy.zzzzzzzz`

### Header

```json
{ 
	"alg": "HS256", 
	"typ": "JWT"
}
```

- `alg` Indicates the signing algorithm
- `typ` The type of this token. i.e., JWT, JWK …etc

### Payload

```json
{ 
	"sub": "1234567890",
	"name": "John Doe", 
	"admin": true 
}
```

The key above were called claims. There are two types of JWT claims.

#### Registered Claim

Registered claim are the standard claims, reserved claims, registered with the [IANA](https://www.iana.org/assignments/jwt/jwt.xhtml) and OIDC standard claims.

[[JWT Standard Claim List]]

#### Custom Claims

These type of claims are defined by third party services or internal usage.

### Signature

The signature is used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.

To create the signature, the Base64-encoded header and payload are taken, along with a secret, and signed with the algorithm specified in the header.

```text
HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)
```

-> imply a hash function with header + payload + secret

## Reference
---

[Auth0 JWT Intro](https://auth0.com/docs/secure/tokens/json-web-tokens/json-web-token-structure)
