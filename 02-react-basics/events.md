# Events

## 1. Concept (Hinglish)
React me events camelCase hote hain (`onClick`) aur handler function reference pass hota hai.

## 2. Why do we need it?
User interaction se state change trigger karne ke liye.

## 3. Laravel Comparison
Blade me form submit server pe jaata hai. React me event browser me handle hota hai, `e.preventDefault()` se default submit rokte hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
`addEventListener` + manual DOM.

## 5. Syntax
```jsx
<button onClick={handleClick}>Save</button>
<form onSubmit={(e) => { e.preventDefault(); save(); }}>
```

## 6. Example
```jsx
<input value={name} onChange={e => setName(e.target.value)} />
```

## 7. Internal Working
React synthetic event system use karta hai: events root par delegate hote hain aur React unhe normalize karke handler ko deta hai.

## 8. Animation / Flow
```text
Browser event -> root par capture -> React handler find -> synthetic event -> handler run
```

## 9. When to use
Click, change, submit, keyboard.

## 10. When NOT to use
Handler me heavy logic inline, uska function alag nikalo.

## 11. Alternatives
Native listeners (`useEffect` me, window/document events ke liye).

## 12. Why this approach / Trade-offs
Declarative handlers component ke saath attach aur cleanup hote hain.

## 13. Common Mistakes
`onClick={fn()}`, preventDefault bhoolna, stale state handlers me.

## 14. Best Practices
Named handlers, args ke liye arrow wrapper.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Synthetic event kya hai?
- Event delegation?
- preventDefault kab?

## 18. Interview English Answer
> React wraps native events in synthetic events and delegates them at the root, so handlers are declared per component and cleaned up automatically.

## 19. Practical Task (solution pehle khud try karo)
Search input + submit form banao jo page reload na kare.

## 20. Revision Points
- camelCase events
- reference pass karo
- preventDefault form me

