# CORS, CSRF, Cookies & Tokens (Laravel Sanctum context)

## 1. Concept (Hinglish)
**CORS:** browser ka cross-origin rule; server headers se allow hota hai. **CSRF:** cookie auth me forged requests ka risk; token se defend. **Cookies/Tokens:** auth carry karne ke tareeke.

## 2. Why do we need it?
React (`localhost:5173`) aur Laravel (`localhost:8000`) alag origins hain, isliye CORS/cookies ka setup chahiye.

## 3. Laravel Comparison
Laravel `config/cors.php`, `VerifyCsrfToken`, Sanctum. Ye Laravel side tumhe pata hoga; naya hai browser ka behavior aur Axios config.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Browser requests block (CORS error).

## 5. Syntax
```php
// config/cors.php
'paths' => ['api/*', 'sanctum/csrf-cookie', 'login', 'logout'],
'allowed_origins' => ['http://localhost:5173'],
'supports_credentials' => true,
```
```env
SANCTUM_STATEFUL_DOMAINS=localhost:5173
SESSION_DOMAIN=localhost
```
```js
export const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,
  withCredentials: true,
  withXSRFToken: true,   // cross-origin dev me XSRF header attach (axios version docs verify karo)
  headers: { Accept: "application/json" },
});
```
Flow (Sanctum SPA): `GET /sanctum/csrf-cookie` -> XSRF-TOKEN cookie -> `POST /login` (header `X-XSRF-TOKEN`) -> session cookie.
Laravel 11+ me `statefulApi()` middleware enable karna padta hai (`bootstrap/app.php`). Exact steps current Laravel docs se verify karo.

## 6. Example
CORS error ka solution backend config hai. Wildcard origin `*` credentials ke saath allowed nahi.

## 7. Internal Working
Cross-origin non-simple request se pehle browser **preflight (OPTIONS)** bhejta hai. Server ko `Access-Control-Allow-Origin` (exact origin) aur `Allow-Credentials: true` dena hota hai.

## 8. Animation / Flow
```text
React -> OPTIONS preflight -> Laravel CORS headers -> actual request (cookies attach) -> response
```

## 9. When to use
Cookie auth: same-site SPA. Bearer token: mobile/3rd-party clients.

## 10. When NOT to use
Token ko localStorage me bina XSS risk samjhe.

## 11. Alternatives
Same-origin deploy (Laravel serve React build) se CORS hi nahi aata; dev proxy (Vite `server.proxy`).

## 12. Why this approach / Trade-offs
Same-site cookie + CSRF protection browser-native hai; token multi-client flexibility deta hai.

## 13. Common Mistakes
CORS frontend se fix karna, `supports_credentials` miss, wildcard origin, 419 CSRF mismatch ignore, domain/port mismatch.

## 14. Best Practices
Dev me Vite proxy, prod me same parent domain, HTTPS.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- CORS kya hai? Preflight?
- CSRF kya hai? Token auth me kyun kam concern?
- Cookie vs token trade-off?
- 401 vs 419?

## 18. Interview English Answer
> CORS is a browser policy that the server relaxes with response headers. With cookie auth I also need CSRF protection and credentials enabled on both sides; with bearer tokens CSRF is less of a concern but XSS exposure of the stored token matters.

## 19. Practical Task (solution pehle khud try karo)
Local me Sanctum SPA setup karo, `/sanctum/csrf-cookie` + `/login` + `/api/user` chala ke dikhao.

## 20. Revision Points
- CORS = server headers
- Preflight OPTIONS
- withCredentials + supports_credentials

