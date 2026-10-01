# DOM Basics

## 1. Concept (Hinglish)
DOM browser ka HTML ka tree representation hai. JS `document` object se elements read/change kar sakta hai.

## 2. Why do we need it?
React ka kaam DOM update karna hi hai. DOM samjho to samajh aata hai ki React kyun virtual tree + diff use karta hai, aur kab direct DOM (refs) chahiye.

## 3. Laravel Comparison
Blade server pe HTML string banata hai. DOM browser me us HTML se bana live object tree hai, jise JS runtime pe badal sakta hai. Ye Laravel me exist hi nahi karta.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Poora page reload ya manual `innerHTML` updates.

## 5. Syntax
```js
const btn = document.querySelector("#save");
btn.addEventListener("click", () => { document.title = "Saved"; });
const li = document.createElement("li"); li.textContent = "Item";
document.querySelector("ul").appendChild(li);
```

## 6. Example
jQuery style: `$('#count').text(count)` har jagah manually. React me `<span>{count}</span>` aur state badlo, React DOM update khud karta hai.

## 7. Internal Working
DOM operations (layout/reflow, repaint) mehngi hoti hain. Bahut saare chhote updates se layout thrashing hota hai. React changes ko compute karke ek commit me apply karta hai.

## 8. Animation / Flow
```text
HTML -> parse -> DOM tree + CSSOM -> render tree -> layout -> paint
```

## 9. When to use
Samajhne ke liye; refs se focus/scroll/measure, third-party libraries integrate karna.

## 10. When NOT to use
React component ke andar `document.querySelector` se UI badalna (React ke control se bahar ho jaata hai).

## 11. Alternatives
React refs (`useRef`), state-driven UI.

## 12. Why this approach / Trade-offs
Declarative UI predictable hai, manual DOM me state aur UI out-of-sync ho jaate hain.

## 13. Common Mistakes
React ke element ko direct mutate karna, har render me `addEventListener` bina cleanup.

## 14. Best Practices
Direct DOM sirf refs/effect me aur cleanup ke saath.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- DOM kya hai? Virtual DOM se kaise alag?
- Event bubbling vs capturing?
- Event delegation kya hai?
- Reflow vs repaint?

## 18. Interview English Answer
> The DOM is the browser's in-memory tree of the page. React avoids manual DOM manipulation by computing the desired UI from state and applying only the necessary changes in one commit.

## 19. Practical Task (solution pehle khud try karo)
1. Vanilla JS me counter banao (DOM manipulation).
2. Wahi React me banao aur dono ka code compare karo.
3. Event delegation se list ke 100 items par ek hi listener lagao.

## 20. Revision Points
- DOM = live tree
- React DOM ko state se derive karta hai
- Manual DOM + React = bugs

