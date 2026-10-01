# Callbacks

## 1. Concept (Hinglish)
Callback ek function hai jo dusre function ko argument me diya jaata hai, taaki wo baad me ya kisi event par call kare.

## 2. Why do we need it?
Array methods (`map`), events (`onClick`), timers aur props me handlers sab callbacks hain. React me child se parent ko communicate karne ka standard tareeka callback prop hai.

## 3. Laravel Comparison
PHP callable (`array_map($fn, ...)`, `Route::get(..., fn() => ...)`) jaisa. Farak: JS me async callbacks (event loop) common hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har cheez hard-coded, reuse nahi.

## 5. Syntax
```js
function fetchData(url, onSuccess, onError) {
  fetch(url).then(r => r.json()).then(onSuccess).catch(onError);
}
setTimeout(() => console.log("done"), 1000);
```

## 6. Example
```jsx
function Child({ onSelect }) { return <button onClick={() => onSelect(5)}>Pick</button>; }
function Parent() { return <Child onSelect={(id) => console.log(id)} />; }
```

## 7. Internal Working
Sync callback usi call stack me chalta hai. Async callback queue me jaata hai aur event loop baad me chalata hai.

## 8. Animation / Flow
```text
Parent callback pass -> Child event -> callback(args) -> Parent state update
```

## 9. When to use
Events, child->parent communication, array helpers.

## 10. When NOT to use
Deeply nested async callbacks (callback hell): Promise/async-await.

## 11. Alternatives
Promises, async/await, custom events.

## 12. Why this approach / Trade-offs
Simple aur universal pattern.

## 13. Common Mistakes
Callback hell, `this` binding confusion, error-first callback me error ignore karna.

## 16. Interview Importance
🟡 MEDIUM — Useful

## 17. Interview Questions
- Callback hell kya hai aur kaise bachte hain?
- Sync vs async callback?

## 18. Interview English Answer
> A callback is a function passed to another function to be invoked later. In React it is the standard way for a child to notify its parent.

## 19. Practical Task (solution pehle khud try karo)
`onChange(value)` callback wala SearchBox component banao jo parent ko value deta ho.

## 20. Revision Points
- Callback = function as argument
- React me child->parent callback prop

