# Arrays & Objects: map, filter, reduce, find, some, every

## 1. Concept (Hinglish)
Array methods data transform karne ke declarative tareeke. `map` transform, `filter` select, `reduce` ek value me combine, `find` pehla match, `some/every` boolean check.

## 2. Why do we need it?
React me list render `map()` se hota hai, search/filter `filter()` se, totals `reduce()` se. Ye methods naya array return karte hain (original mutate nahi), jo React ke immutability model se match karta hai.

## 3. Laravel Comparison
Laravel Collections (`map`, `filter`, `reduce`, `first`, `contains`, `every`) ka direct JS equivalent. Farak: JS arrays me ye built-in hain aur chaining synchronous hoti hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
`for` loops + temporary arrays, zyada verbose aur mutation-prone code.

## 5. Syntax
```js
nums.map(n => n * 2);
nums.filter(n => n > 2);
nums.reduce((sum, n) => sum + n, 0);
users.find(u => u.id === 1);
users.some(u => u.admin); users.every(u => u.active);
```

## 6. Example
```jsx
{users.filter(u => u.active).map(u => <li key={u.id}>{u.name}</li>)}
```

## 7. Internal Working
`map/filter` har element pe callback chalate hain aur naya array banate hain (O(n)). `reduce` accumulator carry karta hai. `find/some/every` match milte hi ruk jaate hain.

## 8. Animation / Flow
```text
[1,2,3] -> map(x*2) -> naya array [2,4,6]; original unchanged
```

## 9. When to use
List rendering, filtering UI, aggregation.

## 10. When NOT to use
Side effects (API call) `map` ke andar mat karo. Bahut bade arrays pe baar-baar chain karne se pehle performance socho.

## 11. Alternatives
`for...of`, `forEach` (return nahi karta), lodash.

## 12. Why this approach / Trade-offs
Declarative code readable hota hai aur React render me expression ki tarah fit hota hai.

## 13. Common Mistakes
`map` me key na dena, `forEach` se JSX return karne ki koshish, `sort()` ko in-place mutate karna state me.

## 14. Best Practices
`[...arr].sort()` ya `toSorted()` use karo state ke liye.

## 15. Wrong vs Better Approach
```js
// Wrong: state mutate
items.sort(); setItems(items);
// Better
setItems([...items].sort());
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- map vs forEach?
- reduce se max find karo.
- find vs filter?
- sort state ko mutate kyun karta hai?

## 18. Interview English Answer
> `map` returns a new array of transformed items, `filter` returns a subset, and `reduce` folds an array into one value. They are non-mutating, which fits React's immutable state updates.

## 19. Practical Task (solution pehle khud try karo)
1. Products array se total price `reduce` se nikalo.
2. Users me active ho aur name search match ho, wo list karo.
3. Duplicate remove karo.

## 20. Revision Points
- map/filter/reduce naya value dete hain.
- sort mutate karta hai.

