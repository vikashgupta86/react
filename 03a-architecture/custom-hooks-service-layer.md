# Custom Hooks, Service Layer, API Layer & Constants

## 1. Concept (Hinglish)
**Service layer:** API calls ek jagah. **Custom hook:** reusable stateful logic. **Constants/utils:** magic strings aur helpers.

## 2. Why do we need it?
Component me axios + state + logic mix ho to test/reuse mushkil.

## 3. Laravel Comparison
Controller -> Service -> Repository pattern jaisa. Yahan: Component -> Hook -> Service -> axios.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Har component me duplicate fetch logic.

## 5. Syntax
```js
// services/employeeService.js
export const employeeService = {
  list: (params) => api.get("/employees", { params }).then(r => r.data),
  create: (payload) => api.post("/employees", payload).then(r => r.data),
};
// hooks/useEmployees.js
export function useEmployees(params) {
  const [state, setState] = useState({ data: [], loading: true, error: null });
  useEffect(() => {
    let ignore = false;
    setState(s => ({ ...s, loading: true }));
    employeeService.list(params)
      .then(res => !ignore && setState({ data: res.data, loading: false, error: null }))
      .catch(e => !ignore && setState({ data: [], loading: false, error: e.message }));
    return () => { ignore = true; };
  }, [JSON.stringify(params)]);
  return state;
}
```
(Production me ye hook React Query se replace karna better hai, dekho state-management notes.)

## 6. Example
constants: `export const ROLES = { ADMIN: "admin", HR: "hr" }`.

## 7. Internal Working
Custom hook ke andar useState/useEffect us component ke hooks list ka hissa banta hai jo hook ko call karta hai.

## 8. Animation / Flow
```text
Component -> useEmployees() -> employeeService -> axios -> Laravel
```

## 9. When to use
Logic reuse, API isolation.

## 10. When NOT to use
Ek baar use hone wale chhote logic ke liye extra abstraction.

## 11. Alternatives
React Query hooks, Redux thunks.

## 12. Why this approach / Trade-offs
Testable, swappable (mock service).

## 13. Common Mistakes
Hook ko shared state samajhna, service me React import, over-abstraction.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Custom hook kab banate ho?
- Service layer ke benefits?

## 18. Interview English Answer
> I keep API calls in a service layer and wrap them with custom hooks so components stay declarative, and the data-access logic is reusable and easy to mock in tests.

## 19. Practical Task (solution pehle khud try karo)
`employeeService` + `useEmployees` banao aur 4 states ke saath use karo.

## 20. Revision Points
- Component -> hook -> service -> axios
- Hook state per caller

