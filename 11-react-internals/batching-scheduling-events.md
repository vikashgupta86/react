# Batching, Scheduling, Fiber & Event System (Deep)

## 1. Concept (Hinglish)
**Batching:** ek event me multiple setState ek render me group. **Scheduling:** React updates ko priority ke saath plan karta hai. **Fiber:** har component ka work unit/node. **Events:** root par delegation.

## 2. Why do we need it?
Isse `setState` ka 'async' behavior, performance aur concurrent features samajh aate hain.

## 3. Laravel Comparison
Laravel queue jobs ko batch/prioritize karna jaisa soch sakte ho (sirf analogy).

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har setState par turant render (slow, inconsistent).

## 5. Syntax
```jsx
function handleClick() {
  setA(1); setB(2); setC(3);   // ek hi re-render (batched)
  console.log(a);              // purani value (snapshot)
}
```
React 18+ me automatic batching (timeouts/promises me bhi). Transitions: `startTransition(() => setQuery(v))` urgent vs non-urgent updates.

## 6. Example
Typing urgent, filtered list render non-urgent: `useTransition`/`useDeferredValue` (docs verify).

## 7. Internal Working
**Render phase:** components call hote hain, naya work-in-progress fiber tree banta hai, diff calculate (interruptible in concurrent rendering). **Commit phase:** DOM mutations apply (synchronous), layout effects, phir passive effects (`useEffect`) schedule hote hain. Events root listener se dispatch hote hain.

## 8. Animation / Flow
```text
setState x3 -> queued -> single render -> reconcile (work-in-progress tree)
-> commit: DOM mutate -> layout effects -> paint -> passive effects
```

## 9. When to use
Debug/perf/interview.

## 10. When NOT to use
Internals ke exact implementation par code depend karna.

## 11. Alternatives
Signals-based frameworks (Solid) alag model.

## 12. Why this approach / Trade-offs
Batching = kam renders, consistent UI.

## 13. Common Mistakes
setState ke baad turant new value expect, render me side effects (concurrent me problem), purity violate.

## 16. Interview Importance
🟠 HIGH (senior rounds 🔥)

## 17. Interview Questions
- Batching kya hai?
- Render vs commit?
- useEffect vs useLayoutEffect?
- Concurrent rendering kya hai?

## 18. Interview English Answer
> React batches state updates triggered in the same tick into one render. Rendering must be pure because React may pause or restart it; DOM changes and effects happen in the commit phase.

## 19. Practical Task (solution pehle khud try karo)
console.log se batching aur effect timing observe karo; useTransition se heavy filter smooth karo.

## 20. Revision Points
- Batching
- Render pure
- Commit = DOM + effects

