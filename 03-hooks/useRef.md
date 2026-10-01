# useRef

## 1. Concept (Hinglish)
`useRef` ek mutable container deta hai (`ref.current`) jo renders ke beech persist karta hai aur change hone pe re-render trigger nahi karta. DOM node access ke liye bhi.

## 2. Why do we need it?
Kabhi value yaad rakhni hoti hai (timer id, previous value) par UI update nahi chahiye.

## 3. Laravel Comparison
Koi direct equivalent nahi. Controller ka instance property jaisa lag sakta hai par yahan sirf component ke life tak, render ke beech.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Globals ya state (extra re-render).

## 5. Syntax
```jsx
const inputRef = useRef(null);
<input ref={inputRef} />
inputRef.current.focus();
```

## 6. Example
```jsx
const timerId = useRef();
timerId.current = setInterval(...);
```

## 7. Internal Working
Ref object `{current}` har render me same rehta hai. `current` mutate karna React ko notify nahi karta. Render ke dauran `ref.current` read/write avoid karo (purity).

## 8. Animation / Flow
```text
ref.current = x -> koi re-render nahi -> next render me bhi same object
```

## 9. When to use
DOM access, timer ids, previous values, non-UI mutable data.

## 10. When NOT to use
Jo value UI me dikhani hai (state use karo).

## 11. Alternatives
useState, module variable.

## 12. Why this approach / Trade-offs
UI trigger nahi chahiye to useRef.

## 13. Common Mistakes
UI value ref me rakhna, render me ref mutate.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- useRef vs useState?
- Ref change par re-render hota hai?

## 18. Interview English Answer
> `useRef` holds a mutable value that persists across renders without causing a re-render, and it is also used to access DOM nodes.

## 19. Practical Task (solution pehle khud try karo)
Input auto-focus aur "previous value" tracker banao.

## 20. Revision Points
- Ref = persist, no re-render
- DOM access

