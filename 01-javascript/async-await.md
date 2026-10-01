# async / await & fetch

## 1. Concept (Hinglish)
`async/await` Promises ke upar syntax sugar hai. `async` function hamesha Promise return karta hai. `await` promise resolve hone tak function ko pause karta hai (baaki program block nahi hota).

## 2. Why do we need it?
React me data fetch async/await se readable hota hai, `try/catch/finally` ke saath loading/error states handle hote hain.

## 3. Laravel Comparison
Laravel me HTTP client ya DB call sync lagti hai. JS me wahi kaam non-blocking hota hai, to loading state UI ka hissa ban jaata hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Lambi `.then` chains, error flow samajhna mushkil.

## 5. Syntax
```js
async function loadUsers() {
  try {
    const res = await fetch("/api/users");
    if (!res.ok) throw new Error("Failed");
    return await res.json();
  } catch (e) { console.error(e); }
  finally { console.log("done"); }
}
```

## 6. Example
```jsx
useEffect(() => {
  const load = async () => { const data = await getUsers(); setUsers(data); };
  load();
}, []);
```
`useEffect(async () => ...)` mat likho, kyunki effect function cleanup return karna chahiye, Promise nahi.

## 7. Internal Working
`await` ke baad ka code microtask me resume hota hai. Function internally promise-returning state machine ban jaata hai.

## 8. Animation / Flow
```text
call async fn -> await fetch() -> function pause, event loop free -> response aaya -> resume -> return value promise me wrap
```

## 9. When to use
Sequential async steps, readable error handling.

## 10. When NOT to use
Independent calls ko ek ke baad ek await karna (slow). Parallel ke liye `Promise.all`.

## 11. Alternatives
`.then` chains.

## 12. Why this approach / Trade-offs
Linear readable code, try/catch se unified error handling.

## 13. Common Mistakes
Sequential await jahan parallel chalega, try/catch bhoolna, `await` loop me bina soche.

## 14. Best Practices
Parallel ho to `Promise.all`. Always handle errors and loading.

## 15. Wrong vs Better Approach
```js
// Wrong: 2 sec + 2 sec
const a = await getA(); const b = await getB();
// Better: parallel
const [a, b] = await Promise.all([getA(), getB()]);
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- async function kya return karta hai?
- useEffect ko async kyun nahi bana sakte?
- Sequential vs parallel await?

## 18. Interview English Answer
> `async/await` is syntactic sugar over Promises that lets me write asynchronous code linearly. An async function always returns a Promise, and I use `Promise.all` for independent requests.

## 19. Practical Task (solution pehle khud try karo)
Ek `fetchUser(id)` likho jo loading, error aur data return kare try/catch/finally ke saath.

## 20. Revision Points
- await = pause function, not thread.
- Parallel = Promise.all.

