# useMemo

## 1. Concept (Hinglish)
`useMemo` expensive calculation ka result cache karta hai jab dependencies same rahein.

## 2. Why do we need it?
Bade filter/sort har render pe dobara compute na ho, ya referential equality stable rahe.

## 3. Laravel Comparison
Laravel cache (`Cache::remember`) jaisa idea, par ye sirf component render ke andar in-memory aur sirf optimization hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har render me recompute.

## 5. Syntax
```jsx
const visible = useMemo(() => items.filter(i => i.name.includes(q)), [items, q]);
```

## 6. Example
Bade table me filter + sort ka result memoize karna.

## 7. Internal Working
React previous deps aur result store karta hai. Deps same (Object.is) to cached result, nahi to compute. React cache drop bhi kar sakta hai, isliye correctness memo pe depend nahi karni chahiye.

## 8. Animation / Flow
```text
render -> deps compare -> same: cached value -> different: recompute
```

## 9. When to use
Measured expensive calculation, memoized child ko stable object dena.

## 10. When NOT to use
Har jagah, simple calculation, bina measure kiye.

## 11. Alternatives
Calculation ko simple rakhna, state structure sudharna, React Compiler (project setup par depend).

## 12. Why this approach / Trade-offs
Memo khud overhead hai, measure karke use karo.

## 13. Common Mistakes
Har value memo karna, deps galat, memo ko correctness ke liye use karna.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- useMemo vs useCallback?
- Kab use nahi karna?

## 18. Interview English Answer
> `useMemo` caches a computed value between renders when its dependencies are unchanged. It is a performance optimization and should be applied after measuring a real cost.

## 19. Practical Task (solution pehle khud try karo)
5000 items ki list pe search filter, useMemo ke saath aur bina, compare karo.

## 20. Revision Points
- Memo = value cache
- Optimization only
- Measure first

