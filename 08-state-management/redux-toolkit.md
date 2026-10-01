# Redux Toolkit

## 1. Concept (Hinglish)
Redux ek predictable global client-state container hai: single store, actions, reducers. Redux Toolkit (RTK) modern official way hai (boilerplate kam).

## 2. Why do we need it?
Bade app me bahut components ko complex shared client state (cart, filters, UI settings) chahiye, aur updates traceable hone chahiye (DevTools).

## 3. Laravel Comparison
Koi seedha equivalent nahi. Event/command + single state tree ka idea; Laravel me state DB me hoti hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Prop drilling ya Context me frequent updates ka re-render issue.

## 5. Syntax
```js
// store.js
import { configureStore, createSlice } from "@reduxjs/toolkit";
const cartSlice = createSlice({
  name: "cart",
  initialState: { items: [] },
  reducers: {
    addItem: (state, action) => { state.items.push(action.payload); },  // Immer: "mutation" safe
    removeItem: (state, action) => { state.items = state.items.filter(i => i.id !== action.payload); },
  },
});
export const { addItem, removeItem } = cartSlice.actions;
export const store = configureStore({ reducer: { cart: cartSlice.reducer } });
// main.jsx
<Provider store={store}><App/></Provider>
// component
const items = useSelector(s => s.cart.items);
const dispatch = useDispatch();
dispatch(addItem(product));
```
`createAsyncThunk` async logic ke liye (ya API data ke liye RTK Query).

## 6. Example
Cart: add/remove/clear, selector se total derive.

## 7. Internal Working
dispatch -> reducer (Immer draft se immutable result) -> store update -> subscribed `useSelector` components jinke selected value change hui wahi re-render.

## 8. Animation / Flow
```text
UI event -> dispatch(action) -> reducer -> new state -> selectors compare -> re-render subscribers
```

## 9. When to use
Large complex client state, many components, traceability needed.

## 10. When NOT to use
Chhote/local state, server data ko copy karke store karna.

## 11. Alternatives
Context+useReducer, Zustand, Jotai, React Query (server state).

## 12. Why this approach / Trade-offs
Selector-based subscription Context se behtar perf; DevTools time travel.

## 13. Common Mistakes
Server state Redux me copy, non-serializable values store me, selectors me naya object return.

## 14. Best Practices
Slices feature-wise, derived data selectors se, RTK Query server state ke liye.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Redux kab use nahi karna?
- Context vs Redux?
- Immer kya karta hai?
- Reducer pure kyun?

## 18. Interview English Answer
> Redux Toolkit provides a single store with slices and selector-based subscriptions, which suits large shared client state. For small or server-derived state I prefer local state, context or a server-state library.

## 19. Practical Task (solution pehle khud try karo)
Cart slice banao (add/remove/qty) + total selector, Redux DevTools se actions dekho.

## 20. Revision Points
- Slice + store + Provider
- Immer
- Server state Redux me nahi

