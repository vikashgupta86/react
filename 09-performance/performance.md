# Performance

## 1. Concept (Hinglish)
Re-render control, Virtual DOM/reconciliation, keys, `React.memo`, `useMemo`, `useCallback`, lazy loading, code splitting, bundle size, pagination, debounce/throttle.

## 2. Why do we need it?
Slow UI user experience kharab karta hai. Par premature optimization bhi problem hai.

## 3. Laravel Comparison
Laravel me N+1/queries/caching optimize karte ho. React me re-render aur bundle size ke saath, aur pehle profile karte hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Poori app ek bundle, har render pe bhaari kaam.

## 5. Syntax
```jsx
const Reports = lazy(() => import("./Reports"));
<Suspense fallback={<Spinner />}><Reports /></Suspense>
const Row = React.memo(function Row({ item }) { ... });
const debounced = useDebounce(search, 300);
```

## 6. Example
Search input me har keystroke pe API: debounce + abort previous request.

## 7. Internal Working
Re-render != DOM update. Component render function chalta hai, React diff karta hai, sirf changed DOM commit hota hai. Render costly ho to problem.

## 8. Animation / Flow
```text
Profile (React DevTools) -> bottleneck find -> fix (structure/memo/split) -> measure again
```

## 9. When to use
Measured problems par optimization.

## 10. When NOT to use
Har jagah memo, bina profile.

## 11. Alternatives
State colocation, virtualization (bade lists), server pagination.

## 12. Why this approach / Trade-offs
Simple fixes (state neeche le jana) aksar memo se behtar.

## 13. Common Mistakes
Everywhere memo, unstable props, bada context, index key, bundle bloat.

## 14. Best Practices
Profile first, lazy routes, virtualize long lists, debounce.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Component 20 baar render ho raha hai, debug kaise?
- memo kab kaam nahi karta?
- Code splitting kya hai?

## 18. Interview English Answer
> I profile first with React DevTools, fix structural causes like misplaced state, then apply memoization, lazy loading or virtualization where measurements show a real benefit.

## 19. Practical Task (solution pehle khud try karo)
Bade list me search + pagination, debounce aur React DevTools se re-renders compare karo.

## 20. Revision Points
- Re-render != DOM update
- Profile first
- Lazy + split

