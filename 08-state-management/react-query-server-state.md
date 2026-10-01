# Server State: React Query (TanStack Query)

## 1. Concept (Hinglish)
Server state = backend ka data jo client me cache hota hai. React Query fetch, cache, dedup, refetch, mutation aur invalidation manage karta hai.

## 2. Why do we need it?
`useEffect + useState` fetch me caching, race conditions, retry, refetch-on-focus manually likhne padte hain. Server state client state se alag nature ka hai: remote, async, stale ho sakta hai, shared ownership.

## 3. Laravel Comparison
Laravel cache (`Cache::remember`) + cache invalidation jaisa idea frontend pe.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual loading/error/data states, duplicate calls, stale data.

## 5. Syntax
```jsx
import { QueryClient, QueryClientProvider, useQuery, useMutation, useQueryClient, keepPreviousData } from "@tanstack/react-query";
const queryClient = new QueryClient();
<QueryClientProvider client={queryClient}><App/></QueryClientProvider>

const { data, isPending, isError, error } = useQuery({
  queryKey: ["employees", { page, search }],
  queryFn: () => employeeService.list({ page, search }),
  placeholderData: keepPreviousData,   // pagination me flicker nahi
});

const qc = useQueryClient();
const createEmployee = useMutation({
  mutationFn: employeeService.create,
  onSuccess: () => qc.invalidateQueries({ queryKey: ["employees"] }),
});
createEmployee.mutate(values);
```
API names versions me badalte hain (v4/v5), current docs verify karo.

## 6. Example
Employee create ke baad list auto refetch (invalidate).

## 7. Internal Working
Query key cache identity hai. Same key ke saare components ek hi request/cache share karte hain. Data `stale` hone par background refetch (focus/reconnect).

## 8. Animation / Flow
```text
useQuery(key) -> cache hit? serve (maybe stale) -> background refetch -> update subscribers
mutate -> success -> invalidate key -> refetch
```

## 9. When to use
API data (almost always).

## 10. When NOT to use
Pure UI state (modal open).

## 11. Alternatives
RTK Query, SWR, manual useEffect.

## 12. Why this approach / Trade-offs
Caching, dedup, retries, invalidation built-in.

## 13. Common Mistakes
Server data Redux/Context me copy, queryKey me dependencies bhoolna, har cheez invalidate.

## 14. Best Practices
Query keys structured, service functions queryFn me, optimistic updates sirf zarurat par.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Server state vs client state?
- Query key ka role?
- Unnecessary API calls kaise rokoge?

## 18. Interview English Answer
> Server state is remote, asynchronous and can go stale, so I manage it with a caching library like React Query using stable query keys and invalidation, and keep Redux or context for genuine client state.

## 19. Practical Task (solution pehle khud try karo)
Employees list + create ko React Query me convert karo; invalidate verify karo.

## 20. Revision Points
- Server state alag
- queryKey = cache identity
- invalidate after mutation

