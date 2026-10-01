# Props

## 1. Concept (Hinglish)
Props parent se child ko diya gaya read-only data hai.

## 2. Why do we need it?
Component reusable banane ke liye: same component alag data ke saath.

## 3. Laravel Comparison
Blade component attributes (`<x-alert type="error"/>`) ~ props. Farak: React props me function, object, JSX bhi pass hota hai, aur props change hone pe re-render hota hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Global variables ya duplicate components.

## 5. Syntax
```jsx
function Button({ label, onClick, variant = "primary" }) {
  return <button className={variant} onClick={onClick}>{label}</button>;
}
<Button label="Save" onClick={save} />
```

## 6. Example
```jsx
<Card title="HRMS"><p>Children props me aata hai</p></Card>
```

## 7. Internal Working
Props ek plain object hai. Parent re-render hota hai to child ko naya props object milta hai. `React.memo` na ho to child bhi re-render hota hai.

## 8. Animation / Flow
```text
Parent state change -> parent re-render -> child ko naye props -> child render
```

## 9. When to use
Parent se child data/handlers dena.

## 10. When NOT to use
Bahut deep levels me pass karna (prop drilling): Context ya composition socho.

## 11. Alternatives
Context, composition (children), state library.

## 12. Why this approach / Trade-offs
Unidirectional data flow debugging aasaan karta hai.

## 13. Common Mistakes
Props mutate karna, props se state copy karna bina reason ke, prop drilling.

## 14. Best Practices
Props read-only, chhota API surface, defaults.

## 15. Wrong vs Better Approach
```jsx
// Wrong
props.user.name = "X";
// Better: parent se callback do aur parent state update kare
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- State vs props?
- Props mutate kyun nahi?
- Prop drilling kya hai?

## 18. Interview English Answer
> Props are read-only inputs passed from a parent to a child component. Data flows one way, so if a child needs to change data, the parent passes a callback.

## 19. Practical Task (solution pehle khud try karo)
Reusable `Button` banao: variant, disabled, onClick, children support ke saath.

## 20. Revision Points
- Props read-only
- One-way data flow
- children bhi prop hai

