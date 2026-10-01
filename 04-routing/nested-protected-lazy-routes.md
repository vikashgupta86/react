# Nested Routes, NavLink, Route Guards, 404, Lazy Routes

## 1. Concept (Hinglish)
Nested routes (layout + child pages), `NavLink` (active styling), guards (auth/role), catch-all 404, lazy loaded route components.

## 2. Why do we need it?
Admin app me shared layout (sidebar + header) aur alag pages hote hain.

## 3. Laravel Comparison
Route groups + middleware (`Route::middleware('auth')->group(...)`) ~ layout route + guard element. Farak: React guard sirf UI render rokta hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har page me layout copy.

## 5. Syntax
```jsx
<Routes>
  <Route path="/login" element={<Login />} />
  <Route element={<RequireAuth />}>              {/* guard layout */}
    <Route element={<AdminLayout />}>            {/* sidebar+header with <Outlet/> */}
      <Route index element={<Dashboard />} />
      <Route path="employees" element={<Employees />} />
      <Route path="employees/:id" element={<EmployeeDetail />} />
      <Route element={<RequireRole roles={["admin"]} />}>
        <Route path="settings" element={<Settings />} />
      </Route>
    </Route>
  </Route>
  <Route path="*" element={<NotFound />} />
</Routes>

function RequireAuth() {
  const { user, loading } = useAuth();
  const location = useLocation();
  if (loading) return <FullPageSpinner />;
  return user ? <Outlet /> : <Navigate to="/login" state={{ from: location }} replace />;
}
function AdminLayout() { return (<div><Sidebar/><main><Outlet/></main></div>); }
<NavLink to="/employees" className={({ isActive }) => isActive ? "active" : ""}>Employees</NavLink>
const Reports = lazy(() => import("./pages/Reports"));
<Suspense fallback={<Spinner/>}><Reports/></Suspense>
```
React Router version me APIs badalti hain (v6/v7), current docs check karo.

## 6. Example
Login ke baad `location.state.from` par redirect.

## 7. Internal Working
Layout route ka element `<Outlet/>` me matching child render karta hai. Lazy route first visit par chunk download karta hai (Suspense fallback tab tak).

## 8. Animation / Flow
```text
URL -> match nested routes -> Guard element -> Layout -> Outlet -> Page
```

## 9. When to use
Admin apps, role-based areas.

## 10. When NOT to use
Role guard ko security samajhna.

## 11. Alternatives
Data routers (loader/action), Next.js.

## 12. Why this approach / Trade-offs
Layout + guard composition reusable.

## 13. Common Mistakes
Auth loading me redirect flash, role check sirf UI, NavLink `end` prop bhoolna.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Outlet kya hai?
- Protected + role-based route?
- Lazy route kab?

## 18. Interview English Answer
> Nested routes let a layout route render child pages through Outlet. Guards are layout elements that redirect when unauthenticated, but the API still enforces real authorization.

## 19. Practical Task (solution pehle khud try karo)
Admin layout + RequireAuth + RequireRole + lazy Reports + 404 banao.

## 20. Revision Points
- Layout route + Outlet
- Guard = UX
- Lazy = code splitting

