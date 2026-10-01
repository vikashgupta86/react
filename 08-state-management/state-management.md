# State Management

## 1. Concept (Hinglish)
Local state, derived state, lifting state up, Context, `useReducer`, Redux Toolkit, client state vs server state.

## 2. Why do we need it?
State kahan rakhein, ye architecture decision hai.

## 3. Laravel Comparison
Laravel me data DB/session me, React me multiple layers: local UI state, shared client state, server state (API cache).

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Prop drilling ya sab kuch global.

## 5. Syntax
Decision tree:
```text
State chahiye
  Sirf ek component? -> useState
  Kuch nearby components? -> Lift state up
  Many components + simple low-frequency value? -> Context
  Complex transitions? -> useReducer
  Bada/complex global client state? -> Redux Toolkit / Zustand
  API/server data? -> React Query/RTK Query (server-state tool)
```

## 6. Example
Theme -> Context. Cart -> reducer/RTK. Employees list from API -> server-state tool, Redux me copy nahi.

## 7. Internal Working
Server state remote hai, stale ho sakta hai, caching/refetch/dedup chahiye. Client state sirf UI ka hai. Dono ko ek tarah manage karna complexity badhata hai.

## 8. Animation / Flow
```text
API data -> cache (React Query) -> components
UI toggles -> local/context state
```

## 9. When to use
Zarurat ke hisaab se sabse simple tool.

## 10. When NOT to use
Redux har chhote state ke liye, Context har frequently changing data ke liye.

## 11. Alternatives
Redux Toolkit, Zustand, Jotai, React Query.

## 12. Why this approach / Trade-offs
Requirement based decision: complexity vs benefit.

## 13. Common Mistakes
API data ko Redux me copy karke manually sync, derived state store karna.

## 14. Best Practices
State minimal, server state alag, colocate state.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- useState vs useReducer vs Context vs Redux kab?
- Server state aur client state alag kyun?
- Redux kab nahi?

## 18. Interview English Answer
> I choose the simplest tool that fits: local state first, lift or use context for shared low-frequency values, a reducer for complex transitions, a store like Redux Toolkit for large client state, and a dedicated library for server state.

## 19. Practical Task (solution pehle khud try karo)
Ek feature (cart + product list) me har state type alag tool se manage karo aur reason likho.

## 20. Revision Points
- Simplest tool first
- Server vs client state
- Derive, don't store

