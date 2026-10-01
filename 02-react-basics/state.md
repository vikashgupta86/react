# State

## 1. Concept (Hinglish)
State component ka aisa data hai jo time ke saath change ho sakta hai. Jab state change hoti hai, React component ko dobara render karta hai taaki UI updated data dikhaye.

## 2. Why do we need it?
Normal variable badalne se UI update nahi hota. State update React ko batata hai ki render karna hai.

## 3. Laravel Comparison
Laravel me state request/session/DB me rehti hai. React state browser memory me component ke andar rehti hai aur refresh pe chali jaati hai. Session state se compare mat karo, ye UI state hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual DOM updates (`element.innerText = count`).

## 5. Syntax
```jsx
const [count, setCount] = useState(0);
<button onClick={() => setCount(count + 1)}>{count}</button>
```

## 6. Example
```jsx
const [form, setForm] = useState({ name: "", email: "" });
setForm(prev => ({ ...prev, name: "Amit" }));
```

## 7. Internal Working
`setState` turant value nahi badalta, update schedule karta hai. Next render me naya state value milti hai. Har render apni snapshot value rakhta hai. Multiple updates batch ho sakte hain.

## 8. Animation / Flow
```text
Click -> handler -> setCount -> update schedule -> render (naya count) -> diff -> commit DOM -> paint
```

## 9. When to use
UI ko change karne wala data.

## 10. When NOT to use
Derived data (compute karo), render ko trigger na karne wali value (`useRef`), server data ke liye dedicated server-state tools.

## 11. Alternatives
useRef, useReducer, Context, Redux, React Query.

## 12. Why this approach / Trade-offs
Simple local data ke liye useState sabse seedha.

## 13. Common Mistakes
State direct mutate, setState ke baad turant naya value expect karna, derived state duplicate karna.

## 14. Best Practices
Minimal state, functional updates, state ko lowest common parent me rakho.

## 15. Wrong vs Better Approach
```jsx
setCount(count + 1); setCount(count + 1); // +1 hi hoga
setCount(c => c + 1); setCount(c => c + 1); // +2
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- State kya hai? Variable se farak?
- setState async kyun lagta hai?
- Functional update kab?

## 18. Interview English Answer
> State is data managed by a component that can change over time and triggers a re-render when updated. Updates are scheduled and batched, so I use functional updates when the next value depends on the previous one.

## 19. Practical Task (solution pehle khud try karo)
Counter + todo list banao, state immutably update karo.

## 20. Revision Points
- Variable badle to UI nahi, state badle to UI
- State snapshot hai
- Functional update

