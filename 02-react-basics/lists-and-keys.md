# Lists & Keys

## 1. Concept (Hinglish)
Array ko `map()` se elements me convert karte hain. Har item ko stable unique `key` chahiye.

## 2. Why do we need it?
Key React ko batati hai ki kaunsa item same hai, taaki sahi DOM/state reuse ho.

## 3. Laravel Comparison
Blade `@foreach` ke jaisa. Farak: React ko identity (key) chahiye diffing ke liye.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Poori list re-create, state mismatch bugs.

## 5. Syntax
```jsx
{users.map(u => <UserRow key={u.id} user={u} />)}
```

## 6. Example
Input wali list me index key use karke reorder karoge to values galat row me chali jaati hain.

## 7. Internal Working
Reconciliation me React same key wale element ko same instance maanta hai aur state preserve karta hai. Key badli to unmount/mount hota hai.

## 8. Animation / Flow
```text
list change -> keys compare -> same key: update, naya key: mount, missing: unmount
```

## 9. When to use
Har dynamic list me.

## 10. When NOT to use
Random key (`Math.random()`) mat use karo.

## 11. Alternatives
Index key sirf static, reorder na hone wali list me.

## 12. Why this approach / Trade-offs
Database id stable aur unique hoti hai.

## 13. Common Mistakes
Index key dynamic list me, random key, key child ke andar ki jagah map ke element par na lagana.

## 14. Best Practices
Stable ID.

## 15. Wrong vs Better Approach
```jsx
{items.map((x, i) => <Item key={i} />)}   // reorder me bug
{items.map(x => <Item key={x.id} />)}      // better
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Key kyun chahiye?
- Index key kab problem?
- Key prop ban kar child ko milti hai?

## 18. Interview English Answer
> Keys give list items a stable identity so React can match items between renders and preserve the correct state. Using indexes in dynamic lists can attach state to the wrong item.

## 19. Practical Task (solution pehle khud try karo)
Editable todo list banao, index key ke saath bug reproduce karo aur id key se fix karo.

## 20. Revision Points
- Key = identity
- Stable unique id
- Index/random avoid

