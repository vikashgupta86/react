# React Internals

## 1. Concept (Hinglish)
Virtual DOM (UI ka lightweight description), reconciliation (diffing), Fiber (React ka internal work unit architecture), render phase vs commit phase, batching, scheduling, synthetic events.

## 2. Why do we need it?
Internals samajhne se performance bugs aur hooks behavior logical lagta hai.

## 3. Laravel Comparison
Laravel request lifecycle (route -> middleware -> controller) jaisa structured flow React ke render/commit lifecycle ke liye mental model de sakta hai, par internals alag hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Direct DOM manipulation, bahut mehnga.

## 5. Syntax
```text
Render phase: components call, new element tree banta hai (pure, interrupt ho sakta hai)
Commit phase: DOM changes apply, layout effects, phir effects
```

## 6. Example
State update -> render -> diff -> commit -> paint.

## 7. Internal Working
Reconciliation heuristics: alag element type to subtree replace; same type to update; lists me key se match. Fiber work ko chhote units me baant kar scheduling (priorities) possible banata hai. Updates batch hote hain. Exact internal implementation versions ke saath badal sakta hai, isliye conceptual model samjho aur docs verify karo.

## 8. Animation / Flow
```text
State Change -> Update Scheduled -> Render Phase -> Reconciliation -> Commit Phase -> DOM Update -> Browser Paint
```

## 9. When to use
Debugging, interviews, perf reasoning.

## 10. When NOT to use
Daily code me internals ke details par depend karna.

## 11. Alternatives
Svelte/Solid compile-time reactivity (different approach).

## 12. Why this approach / Trade-offs
React declarative model: tum describe karte ho, React DOM efficiently update karta hai.

## 13. Common Mistakes
Virtual DOM ko 'always faster' samajhna, re-render = DOM update samajhna.

## 16. Interview Importance
🟠 HIGH — Frequently Asked (senior rounds 🔥)

## 17. Interview Questions
- Virtual DOM kya hai?
- Reconciliation kaise kaam karta hai?
- Fiber kya hai?
- Render vs commit phase?

## 18. Interview English Answer
> Reconciliation compares the previous and next element trees and applies only the necessary DOM changes. Render computes what the UI should be and must be pure; commit applies changes to the DOM.

## 19. Practical Task (solution pehle khud try karo)
Ek component me console.log se render vs commit (effect) order observe karo.

## 20. Revision Points
- Render pure, commit side effects
- Key-based diffing
- Re-render != DOM update

