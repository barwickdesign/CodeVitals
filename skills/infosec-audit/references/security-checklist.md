# Security Checklist

## 1. Secrets & Credentials
- Hardcoded API keys, tokens, passwords, or connection strings in source code
- Secrets in committed .env files or config files
- Secrets in test fixtures, seed data, or example configs
- .gitignore missing entries for .env, credentials, key files
- Secrets visible in CI/CD logs or build output
- Default credentials left in place
- Private keys or certificates in the repository

## 2. Authentication
- Password hashing: is bcrypt/scrypt/argon2 used? What cost factor?
- Password policy enforcement (length, complexity, breach lists)
- Brute force protection: rate limiting on login, account lockout
- Multi-factor authentication availability
- OAuth/OIDC implementation: state parameter, PKCE, token validation
- JWT implementation: algorithm pinning (no "none"), expiry, audience/issuer validation
- Password reset flow: token expiry, single-use, secure delivery
- Session invalidation on password change
- Account enumeration via login/registration/reset responses

## 3. Authorisation
- Broken access control: can users access other users' resources by changing IDs?
- Horizontal privilege escalation: user A accessing user B's data
- Vertical privilege escalation: regular user accessing admin functionality
- Missing authorisation checks on API endpoints
- Insecure Direct Object References (IDOR)
- Role/permission checks: are they centralised or scattered?
- Admin panel protection: separate auth, IP restrictions, audit logging?
- Function-level access control: are all sensitive operations gated?

## 4. Input Validation & Injection
- SQL injection: raw queries with string concatenation/interpolation
- NoSQL injection: unvalidated query operators in MongoDB etc.
- Command injection: user input passed to shell commands, exec, eval
- LDAP injection: user input in LDAP queries
- Template injection: user input rendered in server-side templates
- Path traversal: user input in file paths without sanitisation
- XML External Entity (XXE): XML parsing with external entities enabled
- Deserialisation: untrusted data deserialised without validation
- Request body validation: are schemas enforced? (Zod, Joi, marshmallow, etc.)
- Input length limits: are there max lengths on all text inputs?

## 5. Cross-Site Scripting (XSS)
- Reflected XSS: user input echoed in HTML without encoding
- Stored XSS: user-generated content rendered without escaping
- DOM-based XSS: client-side JS using innerHTML, document.write with user input
- SVG/image upload XSS: SVG files with embedded scripts
- dangerouslySetInnerHTML / v-html / [innerHTML] usage
- Content-Security-Policy header: present and restrictive?
- Template engine auto-escaping: enabled and not bypassed?

## 6. Cross-Site Request Forgery (CSRF)
- CSRF tokens on state-changing endpoints
- SameSite cookie attribute set
- Origin/Referer header validation
- Custom header requirement for API calls
- GET requests performing state changes (anti-pattern)

## 7. Security Headers & Transport
- Strict-Transport-Security (HSTS)
- Content-Security-Policy (CSP)
- X-Content-Type-Options: nosniff
- X-Frame-Options / frame-ancestors
- Referrer-Policy
- Permissions-Policy
- HTTPS enforcement, HTTP redirect
- TLS configuration: minimum version, cipher suites
- CORS: overly permissive origins, credentials exposure

## 8. Cryptography
- Weak algorithms: MD5, SHA1 for security purposes
- Hardcoded encryption keys or IVs
- ECB mode usage (patterns visible in ciphertext)
- Predictable random number generation for security tokens
- Missing salt on password hashes
- Insufficient key length
- Custom crypto implementations (red flag)

## 9. Session Management
- Session ID entropy and unpredictability
- Session fixation: regeneration after login
- Session timeout: idle and absolute
- Secure, HttpOnly, SameSite cookie flags
- Session storage: server-side vs client-side, security of each
- Concurrent session handling
- Session invalidation on logout (server-side)

## 10. File Handling
- Upload type validation: extension only, or magic bytes + MIME?
- Upload size limits enforced
- Uploaded files stored outside webroot
- Filename sanitisation: path traversal, null bytes, special characters
- Virus/malware scanning on uploads
- Image processing: ImageMagick/libvips vulnerability exposure
- Direct file serving vs authenticated download endpoints

## 11. Error Handling & Information Disclosure
- Stack traces exposed in production responses
- Database errors leaked to clients
- Verbose error messages revealing internal paths, versions, or config
- Debug mode enabled in production
- Server version headers exposed
- Directory listing enabled
- Source maps deployed to production
- .git directory accessible

## 12. Dependency Vulnerabilities
- Known CVEs in direct dependencies
- Known CVEs in transitive dependencies
- Abandoned/unmaintained packages with known issues
- Lockfile integrity: is it committed and used in CI?
- Post-install scripts in dependencies (supply chain risk)
- Dependency pinning strategy

## 13. Logging & Monitoring
- Sensitive data in logs: passwords, tokens, PII, credit cards
- Authentication events logged: login, logout, failure, lockout
- Authorisation failures logged
- Log injection: can user input corrupt log format?
- Log storage security and access controls
- Audit trail for sensitive operations
- Alerting on suspicious patterns

## 14. API Security
- Rate limiting on all public endpoints
- Request size limits
- Pagination limits (prevent data dumps)
- GraphQL-specific: query depth limiting, complexity analysis, introspection disabled in prod
- API versioning and deprecation handling
- API key management and rotation
- Webhook signature verification
- Mass assignment / over-posting protection
