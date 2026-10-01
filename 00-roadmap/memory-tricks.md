# Memory Tricks (real concept ka replacement nahi)

| Trick | Accurate explanation |
|---|---|
| State = UI ko change karne wala data | Component-owned data; update par re-render trigger |
| Ref = value hold karo, re-render nahi | Mutable `current`, change par render nahi |
| Memo = result reuse | `useMemo` deps same to cached value |
| Callback = function reference reuse | `useCallback` stable function identity |
| Effect = bahar ki duniya se sync | Render ke baad side effects + cleanup |
| Key = item ka Aadhaar | Stable identity for reconciliation |
| Context = broadcast | Provider value change -> consumers re-render |
| Server state = remote cache | Stale ho sakta hai, cache/invalidate chahiye |
| Guard = UI darwaza, Policy = asli tala | UI hide != security |
