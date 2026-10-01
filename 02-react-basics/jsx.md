# JSX

## 1. Concept (Hinglish)
JSX JavaScript ke andar HTML jaisa syntax hai. Ye HTML nahi, `React.createElement` calls ka syntactic sugar hai.

## 2. Why do we need it?
UI logic aur markup ek saath likhne ke liye, taaki component self-contained rahe.

## 3. Laravel Comparison
Blade `{{ $name }}` ~ JSX `{name}`. `@if/@foreach` ~ JS expressions (`&&`, ternary, `map`). Farak: JSX me full JavaScript expressions chalte hain, Blade me directives.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
String concatenation se HTML banana ya `createElement` manually.

## 5. Syntax
```jsx
const el = <h1 className="title">Hello {user.name}</h1>;
```
Rules: ek parent element (ya `<>...</>`), `class` ke bajay `className`, tags close karo, `{}` me sirf expression.

## 6. Example
```jsx
function Profile({ user }) {
  return (<><h2>{user.name}</h2><p>{user.age >= 18 ? "Adult" : "Minor"}</p></>);
}
```

## 7. Internal Working
Build tool (Babel/esbuild) JSX ko JS function calls me convert karta hai, jo plain objects (React elements) return karte hain. Ye elements UI ka description hain, real DOM nodes nahi.

## 8. Animation / Flow
```text
JSX -> compile -> createElement/jsx() -> React element object -> React ko tree milta hai -> DOM
```

## 9. When to use
Har component ka UI.

## 10. When NOT to use
JSX me heavy logic mat bharo, upar variables me nikalo.

## 11. Alternatives
`createElement`, template literals libraries (htm).

## 12. Why this approach / Trade-offs
Readable aur type-checkable UI code.

## 13. Common Mistakes
`class` likhna, ek parent bhoolna, statement (if) `{}` me likhna, `{}` me object render karna.

## 14. Best Practices
Logic upar, JSX me simple expressions.

## 15. Wrong vs Better Approach
```jsx
// Wrong
<div>{if (ok) { <p>Hi</p> }}</div>
// Better
<div>{ok && <p>Hi</p>}</div>
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- JSX kya hai? Browser samajhta hai?
- JSX vs HTML differences?
- Fragment kyun?

## 18. Interview English Answer
> JSX is a syntax extension that compiles to function calls returning React elements. It is not HTML, so attributes follow JavaScript naming like `className`, and only expressions can appear inside curly braces.

## 19. Practical Task (solution pehle khud try karo)
Ek product card JSX me banao jisme conditional badge ("Sale") ho.

## 20. Revision Points
- JSX = createElement sugar
- {} me expression
- className, fragment

