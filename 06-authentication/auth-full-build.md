# Complete Auth Build: Laravel Sanctum + React

## 1. Concept (Hinglish)
Login, register, logout, current user, protected routes, roles/permissions, 401/419 handling, redirects.

## 2. Why do we need it?
Har real app ka core. Interviews me design question.

## 3. Laravel Comparison
Laravel ka `Auth::attempt`, session, middleware yahan reuse hota hai. React side me auth state aur guards naye hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Server session + Blade `@auth`.

## 5. Syntax
**Laravel**
```php
Route::post('/login', [AuthController::class, 'login']);
Route::middleware('auth:sanctum')->group(function () {
    Route::post('/logout', [AuthController::class, 'logout']);
    Route::get('/user', fn(Request $r) => new UserResource($r->user()));
});
// AuthController
public function login(Request $request) {
    $creds = $request->validate(['email'=>'required|email','password'=>'required']);
    if (!Auth::attempt($creds, $request->boolean('remember'))) {
        throw ValidationException::withMessages(['email' => ['Invalid credentials.']]);
    }
    $request->session()->regenerate();
    return new UserResource($request->user());
}
public function logout(Request $request) {
    Auth::guard('web')->logout();
    $request->session()->invalidate(); $request->session()->regenerateToken();
    return response()->noContent();
}
```
(`/login` ko web/stateful middleware ke saath expose karna padta hai; exact route placement Laravel docs ke hisaab se.)

**React**
```jsx
// authService.js
export const authService = {
  csrf: () => api.get("/sanctum/csrf-cookie"),
  login: async (data) => { await authService.csrf(); return api.post("/login", data).then(r => r.data); },
  me: () => api.get("/api/user").then(r => r.data),
  logout: () => api.post("/logout"),
};
// AuthContext.jsx
export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  useEffect(() => {
    authService.me().then(setUser).catch(() => setUser(null)).finally(() => setLoading(false));
  }, []);
  const login = async (data) => setUser(await authService.login(data));
  const logout = async () => { await authService.logout(); setUser(null); };
  const can = (perm) => user?.permissions?.includes(perm);
  const value = useMemo(() => ({ user, loading, login, logout, can }), [user, loading]);
  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}
// interceptor
api.interceptors.response.use(r => r, err => {
  if (err.response?.status === 401) { window.dispatchEvent(new Event("auth:unauthorized")); }
  return Promise.reject(err);
});
```
Login form: 422 `errors.email` dikhao. Success par `location.state.from ?? "/"` redirect.

## 6. Example
Permission UI: `{can("employee.delete") && <DeleteButton/>}`. Laravel me policy `authorize('delete', $employee)` asli check.

## 7. Internal Working
Refresh -> state reset -> `/api/user` -> cookie se session -> user. Isliye `loading` true se start hota hai.

## 8. Animation / Flow
```text
Login submit -> csrf-cookie -> POST /login -> session cookie -> setUser -> redirect
App load -> GET /user -> 200 user | 401 guest
```

## 9. When to use
SPA same-site: Sanctum cookie.

## 10. When NOT to use
UI permission ko security samajhna.

## 11. Alternatives
Sanctum tokens, Passport, JWT.

## 12. Why this approach / Trade-offs
Session cookie HttpOnly hota hai (JS read nahi kar sakta), XSS se token chori ka risk kam.

## 13. Common Mistakes
Loading state miss (login flash), logout par state/cache clear na karna, 401 loop, permissions sirf frontend.

## 14. Best Practices
HttpOnly cookies, policies, logout cleanup, `remember`, rate limiting login.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Auth flow end to end explain karo.
- Refresh par user kaise milta hai?
- Expired session par kya?
- Role-based UI aur security?

## 18. Interview English Answer
> On app load I call a current-user endpoint to hydrate auth state, route guards handle the UX, and Laravel policies enforce permissions on every API call. On a 401 I clear auth state and redirect to login.

## 19. Practical Task (solution pehle khud try karo)
Login/register/logout + AuthProvider + RequireAuth + role-based menu + 401 handling banao.

## 20. Revision Points
- /user on load
- loading state
- policies backend

