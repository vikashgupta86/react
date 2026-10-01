# Advanced React

## 1. Concept (Hinglish)
Custom hooks, Error Boundaries, Suspense/lazy, Portals, refs/forwardRef, compound components, composition patterns.

## 2. Why do we need it?
Reusable logic aur robust apps ke liye.

## 3. Laravel Comparison
Custom hook ~ Laravel trait/helper/service (logic reuse). Error Boundary ~ exception handler (UI level). Analogy limited hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Duplicate logic, poora app crash.

## 5. Syntax
```jsx
function useDebounce(value, delay = 300) {
  const [v, setV] = useState(value);
  useEffect(() => { const t = setTimeout(() => setV(value), delay); return () => clearTimeout(t); }, [value, delay]);
  return v;
}
createPortal(<Modal/>, document.body);
```
Error Boundary abhi bhi class component se (ya library `react-error-boundary`). Latest React docs verify karo.

## 6. Example
`useFetch`, `useDebounce`, `useLocalStorage`, Modal via Portal.

## 7. Internal Working
Custom hook sirf hooks ka reusable function hai; har component call ka alag state hota hai (state share nahi hota).

## 8. Animation / Flow
```text
component -> custom hook -> useState/useEffect inside -> har caller ka apna state
```

## 9. When to use
Logic duplicate ho raha ho.

## 10. When NOT to use
Bina reuse ke over-abstraction.

## 11. Alternatives
Utility functions, HOC (legacy), render props.

## 12. Why this approach / Trade-offs
Hooks composition simple aur testable.

## 13. Common Mistakes
Custom hook = shared state samajhna, boundary ko event handler errors ke liye expect karna.

## 16. Interview Importance
🟡 MEDIUM — Useful (custom hooks 🟠 HIGH)

## 17. Interview Questions
- Custom hook kab banate ho?
- Error Boundary kya catch nahi karta?

## 18. Interview English Answer
> Custom hooks extract reusable stateful logic, and each call gets its own state. Error boundaries catch rendering errors in their subtree, not errors in event handlers or async code.

## 19. Practical Task (solution pehle khud try karo)
`useDebounce`, `useFetch` banao aur Modal Portal se.

## 20. Revision Points
- Custom hook = logic reuse, not state share
- Boundary limits

