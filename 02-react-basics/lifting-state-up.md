# Lifting State Up

## 1. Concept (Hinglish)
Jab do sibling components ko same data chahiye, state unke nearest common parent me le jaate hain aur props + callbacks se neeche dete hain.

## 2. Why do we need it?
React me data neeche (props) jaata hai. Siblings direct baat nahi karte, isliye shared state parent me hoti hai.

## 3. Laravel Comparison
Shared data controller me ek jagah fetch karke multiple views/partials ko pass karne jaisa idea. Farak: yahan live updates (state change) bhi sync honi chahiye.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Duplicate state, out-of-sync UI.

## 5. Syntax
```jsx
function Parent() {
  const [filter, setFilter] = useState("");
  return (<>
    <SearchBox value={filter} onChange={setFilter} />
    <EmployeeList filter={filter} />
  </>);
}
```

## 6. Example
SearchBox aur List: filter state Parent me. SearchBox `onChange` callback se parent update karta hai.

## 7. Internal Working
Parent state change -> parent re-render -> dono children ko naye props -> dono re-render. Single source of truth.

## 8. Animation / Flow
```text
SearchBox input -> onChange cb -> Parent setFilter -> render -> List naya filter props
```

## 9. When to use
Nearby components shared state.

## 10. When NOT to use
Bahut dur ke components (prop drilling) me: Context ya state library.

## 11. Alternatives
Context, composition (`children`), Redux/Zustand.

## 12. Why this approach / Trade-offs
Simple, explicit data flow.

## 13. Common Mistakes
Dono children me alag copy of state, state bahut upar rakhna jisse unrelated re-renders.

## 14. Best Practices
State ko needed se zyada upar mat le jao, nearest common ancestor.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Lifting state up kab?
- Prop drilling ka solution?

## 18. Interview English Answer
> When multiple components depend on the same data, I move the state to their closest common parent and pass it down with props and callbacks, keeping a single source of truth.

## 19. Practical Task (solution pehle khud try karo)
Product list + cart summary: cart state lift karo aur total dikhao.

## 20. Revision Points
- Nearest common parent
- Single source of truth

