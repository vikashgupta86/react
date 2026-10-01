# Production React

## 1. Concept (Hinglish)
Env variables, dev vs production build, `npm run build`, deployment, API config, error logging, security (XSS, CSRF, CORS), secrets, performance, debugging.

## 2. Why do we need it?
Local pe chalna aur production me safe chalna alag baat hai.

## 3. Laravel Comparison
`.env` + config + `php artisan optimize` ~ Vite `.env` + build. Farak: frontend env variables **bundle me public** ho jaate hain, secrets mat rakho.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Dev server production me.

## 5. Syntax
```bash
# .env.production
VITE_API_URL=https://api.example.com
npm run build   # dist/ static files
```
`VITE_` prefix wale variables client me expose hote hain.

## 6. Example
`dist/` ko Nginx/CDN se serve karo, SPA fallback (`try_files $uri /index.html`).

## 7. Internal Working
Build: bundling, minification, tree-shaking, code splitting, hashed filenames for caching.

## 8. Animation / Flow
```text
React Source -> npm run build -> Bundling -> Optimization -> Static Assets -> Web Server/CDN -> Browser
```

## 9. When to use
CI/CD, env per environment.

## 10. When NOT to use
Secrets frontend env me.

## 11. Alternatives
Vercel/Netlify, Nginx, Laravel public folder me serve.

## 12. Why this approach / Trade-offs
Static hosting cheap aur fast.

## 13. Common Mistakes
Secrets expose, CORS/ cookie domain config galat, SPA fallback miss, source maps public.

## 14. Best Practices
HTTPS, CSP, escape/sanitize HTML (`dangerouslySetInnerHTML` avoid), error monitoring.

## 16. Interview Importance
🟡 MEDIUM — Useful

## 17. Interview Questions
- XSS React me kaise hota hai?
- Env variables safe hain?
- Refresh par 404 kyun?

## 18. Interview English Answer
> React escapes rendered values by default, but XSS is still possible with dangerouslySetInnerHTML or unsafe URLs. Client-side env variables are public, so secrets must stay on the server.

## 19. Practical Task (solution pehle khud try karo)
App build karo, Nginx config me SPA fallback lagao aur env based API URL test karo.

## 20. Revision Points
- VITE_ vars public
- SPA fallback
- XSS avoid raw HTML

