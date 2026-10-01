# Callbacks & Promises

## 1. Concept (Hinglish)
Async kaam (API call, timer) ka result baad me aata hai. **Callback** function pass karna hai. **Promise** ek object hai jo future value represent karta hai: pending, fulfilled ya rejected.

## 2. Why do we need it?
API calls, `useEffect` me data fetch, axios sab Promise based hain.

## 3. Laravel Comparison
PHP synchronous hai (request me line by line). Queue jobs/async HTTP client kuch had tak similar, par JS me async browser ka daily default hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Callback hell (nested callbacks), error handling messy.

## 5. Syntax
```js
fetch("/api/users")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err))
  .finally(() => console.log("done"));
Promise.all([p1, p2]);
```

## 6. Example
```js
const wait = ms => new Promise(resolve => setTimeout(resolve, ms));
wait(1000).then(() => console.log("1s baad"));
```

## 7. Internal Working
Promise callbacks **microtask queue** me jaate hain, jo macrotask (setTimeout) se pehle chalti hai. `.then` hamesha naya promise return karta hai, isliye chaining hoti hai.

## 8. Animation / Flow
```text
fetch() -> pending -> network complete -> fulfilled/rejected -> .then/.catch microtask queue -> call stack khaali hone par run
```

## 9. When to use
Har async operation. Parallel calls ke liye `Promise.all`.

## 10. When NOT to use
Deep `.then` nesting; wahan async/await better.

## 11. Alternatives
Callbacks, async/await, observables (RxJS).

## 12. Why this approach / Trade-offs
Promises error handling aur composition standard deti hain.

## 13. Common Mistakes
`return` bhoolna chain me, `.catch` na lagana, `fetch` me HTTP 404 ko error samajhna (fetch reject nahi karta).

## 14. Best Practices
Hamesha error handle karo. `res.ok` check karo.

## 15. Wrong vs Better Approach
```js
// Wrong: 404 pe bhi then chalega
fetch(url).then(r => r.json())
// Better
fetch(url).then(r => { if (!r.ok) throw new Error(r.status); return r.json(); })
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Promise states?
- Promise.all vs allSettled?
- fetch 404 pe reject hota hai?
- Microtask vs macrotask?

## 18. Interview English Answer
> A Promise represents a value that will be available later, in pending, fulfilled or rejected state. Handlers run as microtasks, and `fetch` only rejects on network failure, so I check `response.ok` explicitly.

## 19. Practical Task (solution pehle khud try karo)
1. 3 API calls parallel karo `Promise.all` se.
2. Ek failing promise ko `catch` karke fallback value do.

## 20. Revision Points
- Promise = future value.
- fetch HTTP error pe reject nahi karta.

