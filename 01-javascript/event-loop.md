# Event Loop, DOM Basics, ES6+

## 1. Concept (Hinglish)
JS single-threaded hai (ek call stack). Event loop decide karta hai ki async callbacks kab chalenge. Queues: **microtask** (promises) aur **macrotask** (setTimeout, events). DOM browser ka tree representation hai HTML ka.

## 2. Why do we need it?
State updates, effects, API responses, aur UI freeze kyun hota hai (heavy sync code), sab event loop se connected hain. React ka rendering/scheduling bhi browser ke event loop ke around kaam karta hai.

## 3. Laravel Comparison
PHP har request me synchronous chalti hai aur khatam. Browser JS long-running event driven environment hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Ya to blocking UI ya multi-thread complexity.

## 5. Syntax
```js
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => console.log(3));
console.log(4);
// 1 4 3 2
```

## 6. Example
```js
document.querySelector("#btn").addEventListener("click", () => console.log("clicked"));
```
React me direct DOM manipulation ki jagah state se UI banate hain.

## 7. Internal Working
Call stack khaali hone par event loop pehle **saari microtasks** chalata hai, phir ek macrotask, phir browser paint kar sakta hai. Isiliye promise `.then`, `setTimeout(0)` se pehle chalta hai.

## 8. Animation / Flow
```text
Sync code (stack) -> stack khaali -> microtasks (promise) -> ek macrotask (timeout/event) -> render/paint -> repeat
```

## 9. When to use
Debugging async order, long tasks se bachna.

## 10. When NOT to use
Heavy loops main thread pe mat chalao (UI freeze). Web Workers consider karo.

## 11. Alternatives
Web Workers, `requestIdleCallback`.

## 12. Why this approach / Trade-offs
Non-blocking model simple hai par sync heavy kaam UI block karta hai.

## 13. Common Mistakes
Order galat predict karna, `setTimeout(0)` ko instant samajhna, heavy compute render me.

## 14. Best Practices
Heavy kaam chunk me ya worker me. Direct DOM mutation React me avoid.

## 15. Wrong vs Better Approach
```js
// Wrong: UI freeze
for (let i = 0; i < 1e9; i++) {}
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Event loop explain karo.
- Microtask vs macrotask?
- Upar ke code ka output aur kyun?

## 18. Interview English Answer
> JavaScript runs on a single thread. After the call stack empties, the event loop drains the microtask queue, such as promise callbacks, before taking the next macrotask like a timer or event.

## 19. Practical Task (solution pehle khud try karo)
3 alag snippets ka output predict karo (setTimeout, promise, sync log mix).

## 20. Revision Points
- Stack -> microtasks -> macrotask.
- Promise.then pehle, setTimeout baad me.

