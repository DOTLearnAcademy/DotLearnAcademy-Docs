# JWT Token Design

**Algorithm:** RS256 (RSA asymmetric signing)  
**Signed by:** Auth Service (private key)  
**Validated by:** All other services (public key via JWKS endpoint)

---

## Access Token

**Expiry:** 15 minutes  
**Storage:** Memory only (never localStorage)

| Claim | Example Value | Purpose |
|-------|--------------|---------|
| sub | "usr_abc123" | User unique ID across all services |
| email | "user@example.com" | Display without extra Auth call |
| role | "Student" / "Instructor" / "Admin" | Used by [Authorize(Roles=)] on all endpoints |
| iat | 1710000000 | Issued-at timestamp |
| exp | iat + 900 (15 min) | Expiry — stateless, no DB lookup needed |
| jti | "uuid-v4" | JWT ID — detect reuse if token stolen |

### DO NOT include in JWT payload:
- Passwords or password hashes
- Full user objects or large data
- Permissions lists (derive from role at service layer)
- Keep payload under 512 bytes

---

## Refresh Token

**Expiry:** 7 days  
**Type:** Opaque UUID (NOT a JWT)  
**Storage:** HttpOnly + SameSite=Strict cookie (never localStorage)

### Rotation Strategy:
1. Client calls POST /auth/refresh with refresh token cookie
2. Auth Service validates token exists in UserDb and is not expired
3. Auth Service issues NEW access token + NEW refresh token
4. Auth Service invalidates the OLD refresh token immediately
5. If a refresh token is used AFTER it was already rotated
   → treat as theft signal
   → invalidate entire token family
   → force user to re-login

---

## JWKS Endpoint

**URL:** GET /auth/.well-known/jwks.json  
**Auth required:** No (public endpoint)  
**Purpose:** Expose RSA public key so all services validate JWTs locally

### How other services use it:
1. On service startup → fetch JWKS endpoint → cache public key in memory
2. Validate every incoming JWT locally using cached public key
3. Zero calls to Auth Service per request at runtime
4. Key rotation: Auth Service publishes old + new key for 24hr overlap
   then removes old key — zero downtime

---

## Password Reset Flow

1. User submits email → POST /auth/password-reset
2. Auth Service generates secure reset token (UUID), stores with 1hr expiry in UserDb
3. Publishes PasswordResetRequested event → SQS → Notification Service
4. Notification Service sends SES email with reset link
5. User clicks link → POST /auth/password-reset/confirm with token + new password
6. Auth Service validates token not expired → hashes new password → invalidates token

---

## Security Rules

- Always RS256 — never HS256 (symmetric keys are dangerous in microservices)
- Access token never stored in localStorage (XSS risk)
- Refresh token in HttpOnly cookie only (JS cannot read it)
- BCrypt work factor 12 for all password hashing
- Rate limit auth endpoints: 10 requests/min per IP