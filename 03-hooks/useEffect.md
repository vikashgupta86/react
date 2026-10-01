# useEffect

## 1. Concept (Hinglish)
`useEffect` render ke baad side effects chalane ka hook hai: API fetch, subscription, timer, document title.

## 2. Why do we need it?
Render pure hona chahiye. External world se sync (network, DOM, timers) effect me hota hai.

## 3. Laravel Comparison
Laravel me controller action ke andar side effects hote hain. React me render ke baad effect chalta hai aur cleanup bhi hota hai. Ye lifecycle hook jaisa dikhta hai par actually 'synchronization' hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Class lifecycle (`componentDidMount/Update/Unmount`).

## 5. Syntax
```jsx
useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id); // cleanup
}, [dep]);
```
Deps: `[]` mount par, `[a,b]` jab change ho, na do to har render par.

## 6. Example
```jsx
useEffect(() => {
  const controller = new AbortController();
  fetch(`/api/users/${id}`, { signal: controller.signal })
    .then(r => r.json()).then(setUser).catch(()=>{});
  return () => controller.abort();
}, [id]);
```

## 7. Internal Working
Render + commit ke baad React effect chalata hai. Dependency array previous render ke saath compare hota hai (`Object.is`). Naya effect chalne se pehle purana cleanup chalta hai. Development Strict Mode me effect extra baar mount/unmount check hota hai, isliye cleanup sahi honi chahiye.

## 8. Animation / Flow
```text
Render -> Commit DOM -> Browser paint -> cleanup (purana) -> effect (naya)
```

## 9. When to use
Subscription, timers, external system sync, fetch (chhote cases).

## 10. When NOT to use
Derived values (render me calculate), event-driven logic (handler me), state ko state se sync karna, bade apps me raw fetch (React Query jaise server-state tool soch sakte ho).

## 11. Alternatives
Event handler, useMemo, React Query/SWR, router loaders.

## 12. Why this approach / Trade-offs
Effect external sync ke liye hai, har kaam ke liye nahi.

## 13. Common Mistakes
Missing deps, infinite loop (effect me state set + dep me wahi state), cleanup bhoolna, object/array dep har render naya, async direct effect function me, race conditions.

## 14. Best Practices
ESLint `react-hooks/exhaustive-deps`, cleanup, AbortController.

## 15. Wrong vs Better Approach
```jsx
useEffect(() => { setCount(count + 1); }, [count]); // infinite loop
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Dependency array kaise kaam karta hai?
- Infinite loop kab?
- Cleanup kab chalta hai?
- Race condition kaise handle?
- Strict Mode me effect 2 baar kyun?

## 18. Interview English Answer
> `useEffect` synchronizes a component with an external system after render. It re-runs when dependencies change, and the cleanup function runs before the next effect and on unmount.

## 19. Practical Task (solution pehle khud try karo)
User details fetch karo `id` badalne par, race condition aur cleanup ke saath.

## 20. Revision Points
- Effect = sync with outside
- Deps = reactive values
- Cleanup before next effect

