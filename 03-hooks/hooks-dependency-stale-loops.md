# Hooks Deep Dive: Dependency Array, Stale Values, Infinite Loops

## 1. Concept (Hinglish)
Ye note `useEffect/useCallback/useMemo` ke 3 sabse zyada interview wale bugs cover karta hai: dependency array, stale closure, infinite loop.

## 2. Why do we need it?
Hooks closures pe based hain. Har render apni values capture karta hai (snapshot). Dependencies React ko batati hain ki kab re-sync karna hai.

## 3. Laravel Comparison
Koi equivalent nahi. Laravel request har baar fresh values ke saath chalti hai, React me purani render ki values closure me reh sakti hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Class lifecycle, manual comparison.

## 5. Syntax
```jsx
useEffect(() => { ... });            // har render ke baad
useEffect(() => { ... }, []);        // sirf mount
useEffect(() => { ... }, [a, b]);    // a ya b badle to
```

## 6. Example
**1. Stale value**
```jsx
useEffect(() => {
  const id = setInterval(() => setCount(count + 1), 1000); // count hamesha 0 capture
  return () => clearInterval(id);
}, []);
// Fix
setCount(c => c + 1);
```
**2. Infinite loop (state in deps + set inside)**
```jsx
useEffect(() => { setList([...list, 1]); }, [list]); // loop
```
**3. Object dep har render naya**
```jsx
const options = { page };             // har render naya object
useEffect(() => load(options), [options]);  // har render chalega
// Fix: primitive dep [page] ya useMemo
```
**4. Race condition**
```jsx
useEffect(() => {
  let ignore = false;
  fetchUser(id).then(u => { if (!ignore) setUser(u); });
  return () => { ignore = true; };
}, [id]);
```

## 7. Internal Working
Har render me effect function naya closure hota hai. React deps ko `Object.is` se compare karta hai. Same -> effect skip. Different -> purana cleanup, phir naya effect. Dependency array me wo saari reactive values aani chahiye jo effect ke andar use hoti hain (ESLint rule `react-hooks/exhaustive-deps` isi ke liye hai).

## 8. Animation / Flow
```text
Render N (values snapshot) -> commit -> deps compare vs Render N-1
 same -> skip effect
 diff -> cleanup(N-1) -> effect(N)
```

## 9. When to use
Deps honestly likho. Functional state update jab previous value chahiye.

## 10. When NOT to use
ESLint warning suppress karke deps hatana. `useEffect` se state se state compute karna (render me derive karo).

## 11. Alternatives
Event handlers, `useMemo`, `useReducer`, `useRef` latest value pattern.

## 12. Why this approach / Trade-offs
Sahi deps = effect hamesha current values ke saath sync.

## 13. Common Mistakes
Deps hata dena, object/array/function dep, async race, setState in effect + dep me wahi state.

## 14. Best Practices
Primitive deps, functional updates, cleanup, AbortController.

## 15. Wrong vs Better Approach
```jsx
useEffect(() => { fetchUsers(filters); }, []);   // filters change par update nahi
useEffect(() => { fetchUsers(filters); }, [filters]); // better (filters stable ho)
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Stale closure kya hai? Fix?
- Infinite loop ke 3 reasons?
- Function dependency ko stable kaise karte ho?
- `ignore` flag vs AbortController?

## 18. Interview English Answer
> Each render captures its own props and state, so an effect created in an older render can see stale values. I fix this by listing real dependencies, using functional updates, and cleaning up effects, rather than suppressing the lint rule.

## 19. Practical Task (solution pehle khud try karo)
1. Stale interval bug reproduce aur fix karo.
2. Infinite loop banao aur 2 tareeke se fix karo.
3. Search fetch me race condition reproduce karke fix karo.

## 20. Revision Points
- Render = snapshot
- Deps = reactive values
- Functional update stale se bachata hai

