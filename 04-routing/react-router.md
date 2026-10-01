# React Router

## 1. Concept (Hinglish)
React Router SPA me URL ke hisaab se alag component dikhata hai bina full page reload ke. Main parts: `BrowserRouter`, `Routes`, `Route`, `Link`, `NavLink`, `useNavigate`, `useParams`, nested routes, protected routes, 404, lazy routes.

## 2. Why do we need it?
SPA me ek hi HTML hota hai, par user ko alag URLs (`/employees/5`) chahiye, bookmark aur back button ke saath.

## 3. Laravel Comparison
Laravel route file (`web.php`) ~ React route config. Farak: Laravel route server pe request resolve karta hai aur controller chalata hai; React Router browser me URL dekhkar component render karta hai. Deep link refresh pe server ko `index.html` serve karna padta hai (fallback).

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual `window.location` aur conditional rendering.

## 5. Syntax
```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/employees/:id" element={<EmployeeDetail />} />
    <Route path="*" element={<NotFound />} />
  </Routes>
</BrowserRouter>
const { id } = useParams();
const navigate = useNavigate();
```
Version specific APIs (data routers, loaders) ke liye official React Router docs check karo.

## 6. Example
```jsx
function ProtectedRoute({ children }) {
  const { user, loading } = useAuth();
  if (loading) return <Spinner />;
  return user ? children : <Navigate to="/login" replace />;
}
const Employees = lazy(() => import("./pages/Employees"));
```

## 7. Internal Working
Router history API (`pushState`) se URL badalta hai bina reload. URL change pe router match karta hai aur matching route ka element render karta hai. `Link` anchor click ko intercept karta hai.

## 8. Animation / Flow
```text
Link click -> pushState -> router URL match -> element render -> page update (no reload)
```

## 9. When to use
SPA navigation, nested layouts, guards.

## 10. When NOT to use
Route guard ko security samajhna: asli security Laravel API me.

## 11. Alternatives
Next.js file routing, TanStack Router.

## 12. Why this approach / Trade-offs
Standard aur large ecosystem.

## 13. Common Mistakes
`<a href>` use karna (reload hota hai), guard ko security maanna, auth loading state na handle karna (flash redirect).

## 14. Best Practices
Layout routes, lazy loading, central route config, 404 route.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Link vs a tag?
- Protected route kaise banate ho? Security kahan?
- Refresh par 404 kyun aata hai deploy me?

## 18. Interview English Answer
> React Router maps URLs to components in the browser using the History API. Protected routes only control the UI, so real authorization must be enforced by the Laravel API.

## 19. Practical Task (solution pehle khud try karo)
Login, Dashboard, Employees, Employee detail, 404 routes + ProtectedRoute banao.

## 20. Revision Points
- Router = URL -> component
- Guard UI only
- SPA fallback server pe

