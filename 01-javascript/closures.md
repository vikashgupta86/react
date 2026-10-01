# Closures, Modules, Optional Chaining, Nullish Coalescing

## 1. Concept (Hinglish)
**Closure:** function jo apne bahar ke variables ko yaad rakhta hai, bahar wala function khatam hone ke baad bhi. **Modules:** `import/export`. **`?.`** safe property access. **`??`** sirf null/undefined par default.

## 2. Why do we need it?
Stale state bug closure se aata hai. Hooks (`useState`, `useEffect`, `useCallback`) closures pe based hain. API data me `user?.profile?.name` roz use hota hai.

## 3. Laravel Comparison
PHP closure me `use ($x)` explicitly capture karna padta hai. JS me capture automatic hota hai. Modules ka similar `use`/`namespace` + autoload hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Global variables, ya data share karne ke liye messy patterns.

## 5. Syntax
```js
function counter() { let c = 0; return () => ++c; }
const inc = counter(); inc(); // 1
inc();                        // 2
const city = user?.address?.city ?? "Unknown";
export const add = (a,b)=>a+b; import { add } from "./math";
```

## 6. Example
```jsx
function Demo() {
  const [count, setCount] = useState(0);
  const alertLater = () => setTimeout(() => alert(count), 3000);
  // click karke 3 sec me count badlo -> alert purani value dikhayega (stale closure)
}
```

## 7. Internal Working
Function banate waqt uska **lexical environment** (scope chain) uske saath attach rehta hai. Har render me naya function bana aur us render ka `count` capture kiya. Isiliye purani value dikhti hai.

## 8. Animation / Flow
```text
Render 1: count=0 -> handler banaya (count=0 capture)
State change -> Render 2: count=1 -> naya handler (count=1)
Purana handler abhi bhi count=0 dekhta hai
```

## 9. When to use
Private state, factories, hooks samajhne ke liye. `??` jab 0/'' valid ho. `?.` unreliable API data me.

## 10. When NOT to use
`||` jab 0 ya empty string valid value ho (`??` use karo).

## 11. Alternatives
Class instance, module-level variable.

## 12. Why this approach / Trade-offs
Closure encapsulation deta hai bina globals ke.

## 13. Common Mistakes
Stale closure, loop me var closure bug, `||` se 0 ko default me badal dena.

## 14. Best Practices
State update me functional form `setCount(c => c + 1)` use karo.

## 15. Wrong vs Better Approach
```js
const qty = input.qty || 1;  // qty=0 bhi 1 ban gaya
const qty = input.qty ?? 1;  // better
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Closure kya hai? Real example?
- Stale closure kya hai?
- `||` vs `??`?
- ES modules vs CommonJS?

## 18. Interview English Answer
> A closure is a function that retains access to variables from its lexical scope even after the outer function has finished. In React, every render creates new closures, which explains stale state bugs when handlers capture old values.

## 19. Practical Task (solution pehle khud try karo)
1. `makeCounter` banao jisme increment/decrement/reset ho.
2. Stale closure ka example likho aur functional update se fix karo.

## 20. Revision Points
- Closure = function + uska scope.
- Hooks closures par based.
- `??` null/undefined ke liye.

