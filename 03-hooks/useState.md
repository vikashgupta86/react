# useState

## 1. Concept (Hinglish)
`useState` function component me state rakhne ka hook hai. Return: `[value, setter]`.

## 2. Why do we need it?
Function har render pe dobara chalta hai, normal variables reset ho jaate hain. React state ko render ke beech yaad rakhta hai.

## 3. Laravel Comparison
Koi direct equivalent nahi. Server request ke beech DB/session rakhta hai, React state component instance ke saath React ke andar store hoti hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Class components me `this.state`, ya globals.

## 5. Syntax
```jsx
const [count, setCount] = useState(0);
const [user, setUser] = useState(() => loadFromStorage()); // lazy init
```

## 6. Example
```jsx
setItems(prev => [...prev, item]);
setUser(prev => ({ ...prev, name }));
```

## 7. Internal Working
React har component ke liye hooks ki **ordered list** rakhta hai. Isiliye hooks conditionally call nahi karte (order same rehna chahiye). Setter update queue me daalta hai, next render me value milti hai. `Object.is` se same value ho to re-render skip ho sakta hai.

## 8. Animation / Flow
```text
setState -> queue -> render -> hooks list se naya value -> JSX -> diff -> commit
```

## 9. When to use
Local UI state: input, toggle, modal.

## 10. When NOT to use
Derived data, mutable value jo render na trigger kare (`useRef`), complex transitions (`useReducer`), server data.

## 11. Alternatives
useReducer, useRef, Context, external store.

## 12. Why this approach / Trade-offs
Sabse simple local state API.

## 13. Common Mistakes
Mutation, stale value, hooks conditional, derived state duplicate, object state me spread bhoolna.

## 14. Best Practices
Functional updates, minimal state, lazy init for expensive init.

## 15. Wrong vs Better Approach
```jsx
const [fullName, setFullName] = useState(first + " " + last); // duplicate
const fullName = first + " " + last;                            // derive
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Hooks ke rules kyun?
- Lazy initialization?
- Same value set karne par re-render?
- State batching?

## 18. Interview English Answer
> `useState` lets a function component keep data between renders. React stores hook state by call order, which is why hooks must be called unconditionally at the top level.

## 19. Practical Task (solution pehle khud try karo)
Toggle, counter, form object state aur lazy init example banao.

## 20. Revision Points
- Order based hooks
- Functional update
- Derive, don't duplicate

