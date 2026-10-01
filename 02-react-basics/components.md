# Components & Functional Components

## 1. Concept (Hinglish)
Component ek reusable function hai jo UI (JSX) return karta hai. Naam capital letter se shuru hota hai.

## 2. Why do we need it?
Bade UI ko chhote reusable tukdon me todne ke liye (Navbar, Card, Table).

## 3. Laravel Comparison
Blade component (`<x-card/>`) ka similar concept. Farak: React component state rakh sakta hai aur apne aap re-render hota hai, Blade component sirf server pe ek baar HTML banata hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Copy-paste HTML ya partials ke saath manual JS wiring.

## 5. Syntax
```jsx
function Card({ title }) { return <div>{title}</div>; }
<Card title="Hello" />
```

## 6. Example
```jsx
function UserList({ users }) {
  return <ul>{users.map(u => <UserItem key={u.id} user={u} />)}</ul>;
}
```

## 7. Internal Working
React component function ko call karta hai, return hue elements se tree banata hai. Component ke andar component define mat karo, har render me naya type ban jaata hai aur state reset ho sakti hai.

## 8. Animation / Flow
```text
<Card/> -> React Card() call karta hai -> JSX return -> tree me add -> DOM
```

## 9. When to use
Reusable UI ya logical section ke liye.

## 10. When NOT to use
Har 3 line ke liye component banana (over-abstraction).

## 11. Alternatives
Class components (legacy), Web Components.

## 12. Why this approach / Trade-offs
Functional components + hooks modern standard hain.

## 13. Common Mistakes
Lowercase naam, nested component definition, ek component me sab kuch.

## 14. Best Practices
Single responsibility, chhote components, meaningful naam.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Component kya hai?
- Functional vs class?
- Component naam capital kyun?

## 18. Interview English Answer
> A component is a reusable function that takes props and returns UI. React calls it during render, and components must be pure with respect to their props and state.

## 19. Practical Task (solution pehle khud try karo)
`Navbar`, `ProductCard`, `ProductList` components banao.

## 20. Revision Points
- Component = function returning JSX
- Capital name
- Nested definition avoid

