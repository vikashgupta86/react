# Production Security: XSS, CSRF, CORS, Auth, Secrets

## 1. Concept (Hinglish)
Frontend security checklist aur Laravel API security jodkar.

## 2. Why do we need it?
Admin/HRMS me sensitive data hota hai.

## 3. Laravel Comparison
Laravel defaults (CSRF, hashing, validation, policies) + frontend risks (XSS, token storage).

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Data leaks.

## 5. Syntax
- **XSS:** React default escape karta hai. Risk: `dangerouslySetInnerHTML`, user URLs (`javascript:`), third-party scripts. Sanitize (DOMPurify), CSP header.
- **CSRF:** cookie auth me Sanctum CSRF token; SameSite cookies.
- **CORS:** exact origins, credentials only jab zarurat.
- **Auth:** HttpOnly + Secure + SameSite cookies, short-lived tokens, rate limit login, policies backend.
- **Secrets:** `VITE_*` public hai, secrets backend only.
- **Dependencies:** `npm audit`, lockfile.
- **Errors:** user ko generic message, logs me detail (Sentry).

## 6. Example
Rich text HTML dikhana ho: `DOMPurify.sanitize(html)` phir hi inject.

## 7. Internal Working
XSS tab hota hai jab untrusted string HTML/JS ban kar execute ho. Token localStorage me ho to XSS usse padh sakta hai; HttpOnly cookie JS se readable nahi.

## 8. Animation / Flow
```text
untrusted input -> sanitize/escape -> render ; secrets backend ; policies on every API call
```

## 9. When to use
Production checklist har release.

## 10. When NOT to use
Security by obscurity.

## 11. Alternatives
WAF, CSP report-only mode.

## 12. Why this approach / Trade-offs
Defense in depth.

## 13. Common Mistakes
UI hide = security, secrets in env, wildcard CORS, tokens in localStorage bina soche.

## 16. Interview Importance
🟡 MEDIUM — Useful (auth security 🟠)

## 17. Interview Questions
- React me XSS kaise possible?
- Token kahan store karte ho aur kyun?

## 18. Interview English Answer
> React escapes values by default, so XSS mainly comes from raw HTML injection and unsafe URLs. I prefer HttpOnly cookies for sessions, keep secrets on the server, and enforce authorization in the API.

## 19. Practical Task (solution pehle khud try karo)
App ka security checklist bana ke audit karo (XSS, CORS, cookies, env, npm audit).

## 20. Revision Points
- Escape/sanitize
- HttpOnly cookies
- VITE_ public

