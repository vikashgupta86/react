# Error, Loading & Empty States, Error Boundaries

## 1. Concept (Hinglish)
Har data screen ki 4 states: loading, error, empty, success. Rendering errors ke liye Error Boundary.

## 2. Why do we need it?
Network slow/fail hota hai. UX professional tab lagta hai jab saari states handle hon.

## 3. Laravel Comparison
Blade me `@forelse ... @empty` aur validation errors. React me ye explicit states hain jo tum manage karte ho.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Blank screen ya crash.

## 5. Syntax
```jsx
function EmployeeList() {
  const { data, loading, error, reload } = useEmployees();
  if (loading) return <Skeleton />;
  if (error) return <ErrorState message={error} onRetry={reload} />;
  if (data.length === 0) return <EmptyState text="No employees" />;
  return <Table rows={data} />;
}
```

## 6. Example
Error boundary (class component ya `react-error-boundary` library) route level pe lagao.

## 7. Internal Working
Error boundary sirf render/lifecycle me errors pakadta hai, event handlers/async code me nahi (wahan try/catch).

## 8. Animation / Flow
```text
fetch start -> loading -> success(data|empty) / failure(error + retry)
```

## 9. When to use
Har API driven screen.

## 10. When NOT to use
Ek global spinner jo sab kuch chhupa de.

## 11. Alternatives
Suspense + error boundary, server-state libs (isPending/isError).

## 12. Why this approach / Trade-offs
Explicit states predictable UX.

## 13. Common Mistakes
Empty state aur loading ko mix karna (flash of empty), error silently ignore.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Loading/empty/error states kaise handle karoge?
- Error boundary kya catch nahi karta?

## 18. Interview English Answer
> Every data-driven view should handle loading, error, empty and success states explicitly, and I add error boundaries at route level to prevent a render error from blanking the whole app.

## 19. Practical Task (solution pehle khud try karo)
Employees list me 4 states implement karo (mock API delay + failure toggle ke saath).

## 20. Revision Points
- 4 states
- Boundary limits
- Retry button

