# Authentication (React + Laravel)

## 1. Concept (Hinglish)
Login, register, logout, current user (`/me`), protected routes, roles/permissions, 401 handling, token/cookie handling.

## 2. Why do we need it?
User identity maintain karni hai jabki React SPA refresh pe memory state kho deti hai.

## 3. Laravel Comparison
Laravel session + middleware (`auth`) ~ React me auth state + route guards + API auth. Farak: asli enforcement Laravel middleware/policies me hota hai; React guard sirf UX.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har page pe server session render.

## 5. Syntax
Option A (SPA cookie, Laravel Sanctum): `GET /sanctum/csrf-cookie` -> `POST /login` -> session cookie -> `GET /api/user`. Same top-level domain/stateful domains config chahiye.
Option B (Token, Sanctum personal access tokens/Passport): login se token -> `Authorization: Bearer`.
```jsx
const AuthContext = createContext(null);
function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  useEffect(() => { api.get("/user").then(r => setUser(r.data)).catch(()=>setUser(null)).finally(()=>setLoading(false)); }, []);
  return <AuthContext.Provider value={{ user, loading, setUser }}>{children}</AuthContext.Provider>;
}
```
Exact setup ke liye current Laravel Sanctum docs verify karo.

## 6. Example
Axios interceptor: 401 aaye to user clear karke `/login` redirect.

## 7. Internal Working
Page refresh -> React state reset -> app start par `/user` call -> cookie/token se Laravel user identify -> state set. Isiliye `loading` state zaroori hai warna login page flash hota hai.

## 8. Animation / Flow
```text
App load -> loading=true -> GET /user -> 200: set user | 401: guest -> loading=false -> routes render
```

## 9. When to use
Cookie auth: same-site SPA. Token: mobile/third-party clients.

## 10. When NOT to use
Token ko blindly localStorage me rakhna (XSS risk), UI role check ko security samajhna.

## 11. Alternatives
Sanctum cookie, Sanctum token, Passport OAuth, JWT.

## 12. Why this approach / Trade-offs
Same-site SPA ke liye Sanctum cookie simple aur safer maana jaata hai; requirements ke hisaab se decide karo.

## 13. Common Mistakes
Auth loading state miss, 401/419 handle na karna, CORS credentials config galat, permissions sirf frontend me.

## 14. Best Practices
Backend policies, short-lived tokens, logout cleanup, HTTPS.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Laravel + React auth design karo.
- Cookie vs token trade-offs?
- Refresh par login kaise persist?
- Role-based UI aur security?

## 18. Interview English Answer
> I would use Sanctum cookie-based auth for a same-site SPA, bootstrap the user via a `/user` endpoint on app load, guard routes in the UI for UX, and enforce authorization with policies on the Laravel API.

## 19. Practical Task (solution pehle khud try karo)
Login/logout/me + ProtectedRoute + role-based menu banao, 401 interceptor ke saath.

## 20. Revision Points
- Refresh pe /user call
- UI guard != security
- Cookie vs token trade-off

