# Functions, Arrow Functions, Template Literals

## 1. Concept (Hinglish)
Function reusable code block hai. JS me function ek **value** hai, variable me store, argument me pass aur return kiya ja sakta hai (first-class functions). Arrow function chhota syntax deta hai aur apna `this` nahi banata.

## 2. Why do we need it?
React component khud ek function hai. Event handlers, callbacks (`map`, `onClick`), custom hooks, sab functions hain. Template literals JSX/strings me `${}` ke liye roz use hote hain.

## 3. Laravel Comparison
PHP closures/arrow fn (`fn($x) => $x*2`) aur callbacks jaise `array_map` ka JS equivalent `map` hai. Farak: JS me function reference pass karna bahut common hai, aur `this` ka behavior PHP se alag hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har baar code copy-paste, ya callbacks ke liye verbose `function(){}` syntax.

## 5. Syntax
```js
function add(a, b) { return a + b; }
const add2 = (a, b) => a + b;
const greet = (name = "Guest") => `Hello ${name}`;
```

## 6. Example
```jsx
function Welcome({ name }) {
  const handleClick = () => alert(`Hi ${name}`);
  return <button onClick={handleClick}>Greet</button>;
}
```

## 7. Internal Working
Function call pe naya **execution context** banta hai (local variables + scope chain). Arrow function lexical `this` use karta hai (jahan define hua wahan ka `this`). Function declaration hoist hoti hai, `const fn = () => {}` TDZ me rehti hai.

## 8. Animation / Flow
```text
fn() call -> naya execution context -> params bind -> body run -> return -> context destroy (agar closure na ho)
```

## 9. When to use
Arrow functions callbacks aur component-level handlers ke liye. Normal function jab hoisting ya apna `this` chahiye.

## 10. When NOT to use
Arrow function ko object method/constructor ki tarah mat use karo (`this` alag hota hai).

## 11. Alternatives
Function declaration vs expression vs arrow.

## 12. Why this approach / Trade-offs
Arrow functions concise hain aur React me `this` problem avoid karte hain kyunki function components me `this` hota hi nahi.

## 13. Common Mistakes
`onClick={handle()}` likhna (render pe call ho jata hai) instead of `onClick={handle}` ya `() => handle(id)`.

## 14. Best Practices
Chhote, ek kaam wale functions. Meaningful naam. Default params use karo.

## 15. Wrong vs Better Approach
```jsx
// Wrong: render ke time call ho gaya
<button onClick={deleteUser(5)}>Del</button>
// Better
<button onClick={() => deleteUser(5)}>Del</button>
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Arrow aur normal function me difference?
- First-class function kya hai?
- `onClick={fn()}` vs `onClick={fn}`?
- Hoisting function declaration vs expression?

## 18. Interview English Answer
> Arrow functions have concise syntax and capture `this` lexically, while regular functions create their own `this` and are hoisted when declared. In React I pass function references to handlers instead of calling them during render.

## 19. Practical Task (solution pehle khud try karo)
1. `sum(...nums)` function likho jo rest use kare.
2. Ek `formatPrice(price, currency="INR")` template literal se banao.
3. Bug batao: `<button onClick={remove(id)}>`.

## 20. Revision Points
- Function = value.
- Arrow = lexical this.
- Handler me reference do, call nahi.

