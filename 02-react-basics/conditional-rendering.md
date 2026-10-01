# Conditional Rendering

## 1. Concept (Hinglish)
Condition ke hisaab se alag UI dikhana.

## 2. Why do we need it?
Loading, error, empty, logged-in/out states handle karne ke liye.

## 3. Laravel Comparison
Blade `@if/@else` ka React equivalent: ternary, `&&`, early return.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
DOM show/hide manual.

## 5. Syntax
```jsx
if (loading) return <Spinner />;
{isAdmin ? <AdminPanel /> : <UserPanel />}
{items.length > 0 && <List items={items} />}
```

## 6. Example
```jsx
if (error) return <ErrorMessage />;
if (!users.length) return <Empty />;
return <UserList users={users} />;
```

## 7. Internal Working
Component alag element type return kare to React purana subtree unmount karke naya mount karta hai (state reset hoti hai). `false/null/undefined` kuch render nahi karte, par `0` render ho jaata hai.

## 8. Animation / Flow
```text
state change -> render -> condition evaluate -> alag JSX -> diff -> mount/unmount
```

## 9. When to use
Loading/error/empty/auth states.

## 10. When NOT to use
Security ke liye (UI hide karna access control nahi).

## 11. Alternatives
Early return, ternary, `&&`, lookup object.

## 12. Why this approach / Trade-offs
Early return readability badhata hai.

## 13. Common Mistakes
`count && <X/>` jab count 0 ho to `0` dikhta hai.

## 15. Wrong vs Better Approach
```jsx
{count && <Badge />}      // 0 dikh sakta hai
{count > 0 && <Badge />}  // better
```

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- `0 &&` bug kya hai?
- UI hide security hai?

## 18. Interview English Answer
> Conditional rendering returns different JSX based on state. I use early returns for loading and error states, and remember that hiding UI is not authorization.

## 19. Practical Task (solution pehle khud try karo)
Loading/error/empty/data 4 states wali user list banao.

## 20. Revision Points
- Early return
- 0 && bug
- UI hide != security

