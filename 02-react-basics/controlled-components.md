# Controlled vs Uncontrolled Components

## 1. Concept (Hinglish)
**Controlled:** input ki value React state se aati hai aur `onChange` se update hoti hai. **Uncontrolled:** value DOM khud rakhta hai, hum `ref`/`FormData` se read karte hain.

## 2. Why do we need it?
Controlled me UI hamesha state ke saath sync hota hai, live validation/formatting possible.

## 3. Laravel Comparison
Blade me `old('name')` se value restore karte ho. Yahan state hi wo value hai jo har keystroke pe update hoti hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual DOM value reads.

## 5. Syntax
```jsx
// controlled
<input value={name} onChange={e => setName(e.target.value)} />
// uncontrolled
const ref = useRef(); <input ref={ref} defaultValue="x" />  // ref.current.value
```

## 6. Example
File input hamesha uncontrolled hota hai (security). Uncontrolled bade forms me `FormData(e.target)` se read karte hain.

## 7. Internal Working
Controlled me `value` prop dene par React DOM ki value ko state se force karta hai. `value` ke bina `onChange` doge to input read-only jaisa behave karega (warning).

## 8. Animation / Flow
```text
keystroke -> onChange -> setState -> render -> input.value = state
```

## 9. When to use
Controlled: validation, dependent fields, live UI. Uncontrolled: simple forms, file inputs.

## 10. When NOT to use
Controlled bahut heavy forms me bina optimization.

## 11. Alternatives
React Hook Form (mostly uncontrolled + refs).

## 12. Why this approach / Trade-offs
Controlled predictable, uncontrolled kam re-renders.

## 13. Common Mistakes
`value` ke saath `defaultValue`, `null` value, onChange miss.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Controlled vs uncontrolled?
- File input controlled kyun nahi?
- Controlled form me performance issue kab?

## 18. Interview English Answer
> In a controlled component, React state is the single source of truth for the input value. In an uncontrolled one, the DOM holds the value and we read it with refs or FormData.

## 19. Practical Task (solution pehle khud try karo)
Same signup form ko controlled aur uncontrolled dono tareeke se banao.

## 20. Revision Points
- Controlled = state owns value
- Uncontrolled = DOM owns value

