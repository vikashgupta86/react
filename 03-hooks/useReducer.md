# useReducer

## 1. Concept (Hinglish)
`useReducer` complex state transitions ko ek reducer function me organize karta hai: `(state, action) => newState`.

## 2. Why do we need it?
Jab state ke multiple fields aur many update types hon, `useState` scattered ho jaata hai.

## 3. Laravel Comparison
Event/action ko state transition me map karna thoda Laravel ke state machine / command pattern jaisa idea hai, par ye sirf UI state ke liye hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Bahut saare setState calls.

## 5. Syntax
```jsx
function reducer(state, action) {
  switch (action.type) {
    case "add": return { ...state, items: [...state.items, action.item] };
    default: return state;
  }
}
const [state, dispatch] = useReducer(reducer, { items: [] });
dispatch({ type: "add", item });
```

## 6. Example
Cart: add, remove, clear, qty update.

## 7. Internal Working
Dispatch action queue karta hai, React reducer run karke naya state nikalta hai. Reducer pure hona chahiye (no API call, no mutation).

## 8. Animation / Flow
```text
dispatch(action) -> reducer(state, action) -> new state -> render
```

## 9. When to use
Related fields, many transitions, testable logic.

## 10. When NOT to use
Simple toggle/counter.

## 11. Alternatives
useState, Redux Toolkit, Zustand.

## 12. Why this approach / Trade-offs
Logic ek jagah, testable, predictable.

## 13. Common Mistakes
Reducer me mutation/side effects, default case miss.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- useState vs useReducer?
- Reducer pure kyun?

## 18. Interview English Answer
> `useReducer` centralizes state transitions in a pure reducer function. I choose it when state has multiple related fields or many update types.

## 19. Practical Task (solution pehle khud try karo)
Shopping cart reducer likho (add/remove/update qty/clear).

## 20. Revision Points
- Reducer pure
- Action driven updates

