# React.memo, Debounce, Throttle, Code Splitting & Bundle Size

## 1. Concept (Hinglish)
`React.memo` props same ho to re-render skip. Debounce: last event ke X ms baad run. Throttle: max har X ms me ek baar. Code splitting: bundle ko chunks me tod kar lazy load.

## 2. Why do we need it?
Unnecessary renders, har keystroke API calls aur bada bundle slow UX dete hain.

## 3. Laravel Comparison
Query/response caching aur rate limiting jaisa idea: kam kaam, sahi time par.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har render pe poori tree, ek bada JS bundle.

## 5. Syntax
```jsx
const Row = React.memo(function Row({ employee, onSelect }) { ... });
const onSelect = useCallback((id) => setSelected(id), []);

function useDebounce(value, delay = 400) {
  const [v, setV] = useState(value);
  useEffect(() => { const t = setTimeout(() => setV(value), delay); return () => clearTimeout(t); }, [value, delay]);
  return v;
}
// throttle (scroll/resize): utility lodash.throttle ya custom
const Reports = lazy(() => import("./Reports"));
```
Bundle analyze: `npx vite-bundle-visualizer` (tool docs verify).

## 6. Example
Search input me `useDebounce(search)` ko query key me use karo.

## 7. Internal Working
`React.memo` props ko shallow compare karta hai. Naya object/function prop har render => memo bekaar. Isliye `useCallback/useMemo` sirf memoized child ke saath meaningful.

## 8. Animation / Flow
```text
Parent render -> props shallow compare -> same? skip child : render child
```

## 9. When to use
Measured heavy lists/rows, expensive subtrees; route-level splitting.

## 10. When NOT to use
Har component me memo.

## 11. Alternatives
State colocation, virtualization (`react-window`), pagination.

## 12. Why this approach / Trade-offs
Pehle structure fix, phir memo.

## 13. Common Mistakes
Unstable props, memo + children prop (har render naya), premature optimization.

## 14. Best Practices
Profile -> fix -> measure.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- React.memo kab kaam nahi karta?
- Debounce vs throttle?
- Bundle size kaise kam?

## 18. Interview English Answer
> React.memo skips re-rendering when props are shallowly equal, so it only helps if the props are stable. I debounce search input, split bundles by route and optimize only after profiling.

## 19. Practical Task (solution pehle khud try karo)
5000 row list: bina memo vs memo + useCallback compare (Profiler), phir virtualize.

## 20. Revision Points
- memo = shallow props compare
- debounce vs throttle
- lazy chunks

