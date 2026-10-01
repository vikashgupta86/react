# Destructuring, Spread, Rest

## 1. Concept (Hinglish)
Destructuring array/object se values nikalne ka short tareeka. Spread (`...`) values phailata hai (copy/merge). Rest (`...`) bachi hui values ikatthi karta hai.

## 2. Why do we need it?
Props destructuring (`function Card({title})`), `useState` ka `[a,b]`, aur immutable state updates (`{...user, name}`) sab isi se hote hain.

## 3. Laravel Comparison
PHP `[$a,$b] = $arr` aur `extract()` / array spread `[...$a, ...$b]` similar hain. Farak: JS object destructuring property name se hoti hai, aur spread shallow copy deta hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
`const name = user.name; const age = user.age;` repetitive, aur state copy karna verbose.

## 5. Syntax
```js
const { name, age = 18 } = user;
const [first, ...others] = list;
const updated = { ...user, name: "Neha" };
const merged = [...a, ...b];
```

## 6. Example
```jsx
function Card({ title, price }) { return <h3>{title}: {price}</h3>; }
setUser(prev => ({ ...prev, name: "Neha" }));
setItems(prev => [...prev, newItem]);
```

## 7. Internal Working
Destructuring syntactic sugar hai, engine property access karke variables bana deta hai. Spread **shallow copy** karta hai: nested object ka reference same rehta hai.

## 8. Animation / Flow
```text
{...user, name:"X"} -> naya object -> user ki properties copy -> name override -> naya reference -> React ko change dikhta hai
```

## 9. When to use
Props, state updates, function params, API response se fields nikalna.

## 10. When NOT to use
Deep nested objects ko spread se deep copy samajhna. Bahut deep destructuring jo code unreadable bana de.

## 11. Alternatives
`Object.assign`, `structuredClone`, immer library.

## 12. Why this approach / Trade-offs
Immutable update ke liye spread simple hai. Deep nested update bar-bar ho to immer ya structure flatten karna better.

## 13. Common Mistakes
Nested state ko direct mutate karna, spread ko deep copy samajhna.

## 14. Best Practices
State hamesha naya object/array banake update karo.

## 15. Wrong vs Better Approach
```js
// Wrong
user.name = "Neha"; setUser(user);   // same reference, re-render skip ho sakta hai
// Better
setUser({ ...user, name: "Neha" });
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Spread aur rest me farak?
- Shallow vs deep copy?
- State mutate karne se kya problem?

## 18. Interview English Answer
> Destructuring extracts values from arrays or objects, spread expands them for copying or merging, and rest collects remaining items. Spread makes a shallow copy, so for nested state I update each level immutably.

## 19. Practical Task (solution pehle khud try karo)
1. Nested object `{user:{address:{city}}}` ka city immutably update karo.
2. Function jo first item aur baaki alag return kare (rest).

## 20. Revision Points
- Spread = shallow copy.
- State replace karo, mutate nahi.

