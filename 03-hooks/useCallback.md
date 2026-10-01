# useCallback

## 1. Concept (Hinglish)
`useCallback` function ka reference render ke beech stable rakhta hai (deps same ho to).

## 2. Why do we need it?
`React.memo` wale child ko naya function prop milta hai har render to memo bekaar ho jaata hai. Stable reference se skip possible.

## 3. Laravel Comparison
Direct equivalent nahi. Ye reference identity ka concept hai, jo PHP me aam taur par matter nahi karta.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har render naya function.

## 5. Syntax
```jsx
const handleSave = useCallback((id) => save(id), [save]);
<Child onSave={handleSave} />
```

## 6. Example
`React.memo(Child)` ke saath use karna.

## 7. Internal Working
`useCallback(fn, deps)` ~ `useMemo(() => fn, deps)`. Function har render me banta hi hai, hook sirf purana reference return karta hai.

## 8. Animation / Flow
```text
render -> deps same? -> purana function reference -> memo child skip
```

## 9. When to use
Memoized child ko handler dena, effect dependency stable rakhna.

## 10. When NOT to use
Jahan child memoized nahi hai, har handler pe.

## 11. Alternatives
Function ko effect/component ke andar ya bahar move karna.

## 12. Why this approach / Trade-offs
Sirf tab fayda jab reference equality kisi jagah matter kare.

## 13. Common Mistakes
Bina React.memo ke use, deps galat (stale closure).

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- useCallback kab fayda deta hai?
- Stale closure kaise aata hai isme?

## 18. Interview English Answer
> `useCallback` returns a stable function reference between renders. It helps only when something depends on reference equality, such as a memoized child or an effect dependency.

## 19. Practical Task (solution pehle khud try karo)
Memoized child banao jo bina useCallback ke re-render ho, phir fix karo.

## 20. Revision Points
- Callback = function reference cache
- React.memo ke saath meaningful

