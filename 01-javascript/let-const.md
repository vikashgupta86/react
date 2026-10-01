# let, const, var

## 1. Concept (Hinglish)
Variable declare karne ke 3 tareeke. Farak: scope, re-assign aur hoisting.

| | var | let | const |
|---|---|---|---|
| Scope | Function | Block | Block |
| Re-assign | Haan | Haan | Nahi |
| Re-declare | Haan | Nahi | Nahi |
| Hoisting | `undefined` ke saath | TDZ | TDZ |

## 2. Why do we need it?
React me `const [count, setCount] = useState(0)` roz dikhta hai. Har render pe component function dobara chalta hai aur naya `count` variable banta hai, isliye `const` chal jaata hai. `var` ki problem: block se leak hota tha, accidental overwrite hota tha.

## 3. Laravel Comparison
PHP `$var` me bhi `if/for` block naya scope nahi banata (var jaisa). Par PHP me hoisting nahi hai. PHP constants deep locked hote hain, JS `const` sirf binding lock karta hai, object mutate ho sakta hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
IIFE hacks aur scope collision bugs.

## 5. Syntax
```js
var a = 1; let b = 2; const c = 3;
b = 20;  // ok
c = 30;  // TypeError
```

## 6. Example
```js
const user = { name: "Amit" };
user.name = "Ravi"; // ok, object mutate hua
user = {};          // error, binding change
```

## 7. Internal Working
Creation phase: `var` ko memory + `undefined`. `let/const` ko memory lekin uninitialized (TDZ). Execution phase me declaration line pe TDZ khatam hota hai.
```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 3 3 3
for (let i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 0 1 2
```
`let` har iteration ke liye naya binding banata hai, isliye har closure apna `i` yaad rakhta hai.

## 8. Animation / Flow
```text
Code run -> Creation phase (var=undefined, let/const=TDZ) -> Execution
-> declaration line -> accessible -> block end -> let/const scope se bahar
```

## 9. When to use
Default `const`. Reassign hona ho (counter, flag) to `let`.

## 10. When NOT to use
`var` modern code me nahi. `const` ko deep immutable mat samjho. `let` jahan `const` chal jaye wahan mat use karo.

## 11. Alternatives
`Object.freeze()` shallow immutability ke liye. Legacy code me `var`.

## 12. Why this approach / Trade-offs
`const` padhne wale ko batata hai ki binding change nahi hogi, isse reasoning aur debugging aasaan hoti hai. React me state ko mutate nahi, replace karte hain, ye mindset isi se aata hai.

## 13. Common Mistakes
const = immutable samajhna; TDZ me access; loop me var + async callback; sab kuch let bana dena.

## 14. Best Practices
Pehle const, zaroorat par let, var avoid. ESLint `prefer-const` on rakho.

## 15. Wrong vs Better Approach
```js
// Wrong
for (var i = 0; i < items.length; i++) {}
console.log(i); // leak
// Better
for (let i = 0; i < items.length; i++) {}
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Beginner: let, const, var me difference?
- Intermediate: Hoisting aur TDZ kya hai?
- Advanced: var wale loop + setTimeout ka output kyun 3 3 3?
- Tricky: `const arr=[]; arr.push(1)` chalega?
- Follow-up: Kya let hoisted hota hai?

## 18. Interview English Answer
> `var` is function-scoped and hoisted as `undefined`, while `let` and `const` are block-scoped and sit in the temporal dead zone until declared. `const` prevents reassignment but not mutation. I default to `const`, use `let` when reassignment is needed, and avoid `var`.

## 19. Practical Task (solution pehle khud try karo)
1. `console.log(x); var x=5; console.log(y); let y=10;` output predict karo.
2. `const user={name:"Ravi"}; user.name="Amit"; user={};` kya hoga?
3. `var` wale loop ko ek chhote change se `0 1 2` print karwao.
4. `const [count,setCount]=useState(0)` me const kaise chalta hai?

## 20. Revision Points
- Default const, phir let.
- TDZ = declare se pehle access error.
- const binding lock karta hai, object nahi.

