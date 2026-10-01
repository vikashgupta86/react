# Module 3: Layout, Routing & Guards

## Requirement
Sidebar + header layout, protected routes, 404, active menu.

## React concepts
Nested routes, `Outlet`, `NavLink`, guard layout, lazy routes.

## Implementation
Use code from `04-routing/nested-protected-lazy-routes.md`.
```jsx
const menu = [
  { to: "/", label: "Dashboard", end: true },
  { to: "/employees", label: "Employees", perm: "employee.view" },
];
{menu.filter(m => !m.perm || can(m.perm)).map(m => (
  <NavLink key={m.to} to={m.to} end={m.end}>{m.label}</NavLink>
))}
```

## Flow
URL -> guard (auth) -> layout -> Outlet -> page.

## Task
Admin layout, guard, role-based menu, lazy Reports page, 404.

## Interview Qs
- Outlet kya hai?
- Menu hide karna security hai?
