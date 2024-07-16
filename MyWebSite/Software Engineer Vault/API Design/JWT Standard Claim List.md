---
created: 2024-01-08 23:02
aliases:
  - jwt claims
tags: 
card link:
  - "[[JWT]]"
source:
---
## Description
---

The claims below are commonly used reserved claims. Others can be found at [Internet Assigned Number Authority|IANA](https://www.iana.org/assignments/jwt/jwt.xhtml)

- `iss` (issuer): Issuer of the JWT
- `sub` (subject): Subject of the JWT (the user)
- `aud` (audience): Recipient for which the JWT is intended
- `exp` (expiration time): Time after which the JWT expires
- `nbf` (not before time): Time before which the JWT must not be accepted for processing
- `iat` (issued at time): Time at which the JWT was issued; can be used to determine age of the JWT
- `jti` (JWT ID): Unique identifier; can be used to prevent the JWT from being replayed (allows a token to be used only once)




## Reference
---





