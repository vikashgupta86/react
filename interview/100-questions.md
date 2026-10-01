# React Interview: 100 Questions

25 Beginner + 30 Intermediate + 25 Advanced + 20 Scenario. Important questions me detailed answer, follow-up aur common wrong answer bhi hai.

## Beginner (1-25)

**1. React kya hai?**
- Short answer: Component-based declarative library for building UIs.

**2. React library hai ya framework?**
- Short answer: Library; routing, data fetching etc. ecosystem se aate hain.

**3. JSX kya hai?**
- Short answer: createElement calls ka syntax sugar, HTML nahi.

**4. Virtual DOM kya hai?**
- Short answer: UI ka in-memory description jise diff karke minimal DOM update hota hai.

**5. Component kya hai?**
- Short answer: Reusable function jo props leke UI return karta hai.

**6. Functional vs class component?**
- Short answer: Modern code functional + hooks; class legacy.

**7. Props kya hain?**
- Short answer: Parent se child ko read-only inputs.

**8. State kya hai?**
- Short answer: Component-owned data; change par re-render.

**9. Props vs state?**
- Short answer: Props external read-only, state internal mutable-via-setter.
- Detailed: Props read-only inputs; state owned data triggers re-render.
- Example: Parent state -> child props
- Follow-up: Child props ko state me copy karna kab theek?
- Common wrong answer: 'Props mutable hain'

**10. Keys kyun?**
- Short answer: List items ki stable identity for reconciliation.

**11. Index ko key kab nahi?**
- Short answer: Jab list reorder/insert/delete ho sakti ho.

**12. Controlled component?**
- Short answer: Input jiski value React state control karti hai.

**13. Uncontrolled?**
- Short answer: DOM value rakhta hai, ref/FormData se padhte hain.

**14. Conditional rendering kaise?**
- Short answer: Ternary, &&, early return.

**15. Fragment kyun?**
- Short answer: Extra DOM wrapper ke bina multiple elements return.

**16. Event handling React me?**
- Short answer: camelCase props, synthetic events, function reference pass.

**17. SPA kya hai?**
- Short answer: Ek HTML page, JS se navigation/updates.

**18. CSR vs SSR?**
- Short answer: Browser me render vs server pe HTML render.

**19. npm kya hai?**
- Short answer: Package manager.

**20. Vite kya hai?**
- Short answer: Fast dev server + bundler.

**21. Fast refresh/HMR?**
- Short answer: Code change par page reload ke bina module replace.

**22. `onClick={fn()}` galat kyun?**
- Short answer: Render me call ho jata hai; reference do.

**23. Lifting state up?**
- Short answer: Shared state nearest common parent me.

**24. Prop drilling?**
- Short answer: Deep levels me props pass; Context/composition se kam.

**25. Why can't mutate state?**
- Short answer: React new reference se change detect karta hai.

## Intermediate (26-55)

**26. useEffect dependency array?**
- Short answer: Deps change par cleanup+effect; Object.is compare.
- Detailed: React previous aur current deps Object.is se compare karta hai; change par cleanup phir effect.
- Example: `[id]` badle to fetch dobara
- Follow-up: Function dep ko stable kaise?
- Common wrong answer: 'Sirf performance ke liye hai'

**27. useEffect empty array?**
- Short answer: Sirf mount par (aur Strict Mode dev me extra check).

**28. Cleanup function kab?**
- Short answer: Next effect se pehle aur unmount par.

**29. Infinite loop in effect?**
- Short answer: State set + wahi dep, ya unstable object/array/function dep.

**30. Stale closure?**
- Short answer: Purani render ki value capture; functional update/deps.
- Detailed: Handler/effect purani render ki state capture karta hai.
- Example: `setCount(c=>c+1)`
- Follow-up: useRef latest value pattern?
- Common wrong answer: 'React bug hai'

**31. useRef vs useState?**
- Short answer: Ref re-render nahi karta.

**32. useMemo?**
- Short answer: Value cache; optimization only.

**33. useCallback?**
- Short answer: Function reference cache.

**34. useMemo vs useCallback?**
- Short answer: Value vs function.

**35. React.memo?**
- Short answer: Props shallow equal to re-render skip.

**36. useContext issue?**
- Short answer: Value change par saare consumers re-render.

**37. useReducer kab?**
- Short answer: Complex related transitions.

**38. Batching?**
- Short answer: Same tick me multiple setState ek render.

**39. setState async?**
- Short answer: Scheduled/batched, value next render me.

**40. Functional update kab?**
- Short answer: Next value previous par depend kare.

**41. Derived state anti-pattern?**
- Short answer: State se compute hone wali value state me store mat karo.

**42. Custom hook?**
- Short answer: Reusable stateful logic function; state per caller.

**43. Error boundary?**
- Short answer: Render errors pakadta hai, event/async nahi.

**44. Lazy + Suspense?**
- Short answer: Component code-split, fallback jab tak load.

**45. Protected route?**
- Short answer: Auth check + Navigate; security API me.

**46. Link vs a?**
- Short answer: Link reload nahi karta.

**47. useNavigate/useParams?**
- Short answer: Programmatic nav / URL params.

**48. Controlled form validation?**
- Short answer: State + errors + submit validate; server 422 map.

**49. Debounce?**
- Short answer: Typing ruke tab call.

**50. Pagination server-side kyun?**
- Short answer: Bade data ke liye.

**51. CORS kya?**
- Short answer: Browser cross-origin policy; server headers.

**52. 401 vs 403 vs 422?**
- Short answer: Unauthenticated, forbidden, validation.

**53. Axios interceptor use?**
- Short answer: Common auth/error handling.

**54. Context vs Redux?**
- Short answer: Simple shared vs large selector-based store.
- Detailed: Context shared value, consumers re-render; Redux selector subscriptions+devtools.
- Example: Theme vs cart
- Follow-up: Zustand?
- Common wrong answer: 'Redux replacement hai Context'

**55. Server vs client state?**
- Short answer: Remote stale cache vs UI state.
- Detailed: Server remote/stale/shared ownership; client UI-only.
- Example: React Query vs useState
- Follow-up: Invalidate kab?
- Common wrong answer: 'Sab Redux me daalo'

## Advanced (56-80)

**56. Reconciliation?**
- Short answer: Type+key heuristics diff.
- Detailed: Same type update, alag type replace, list me key match.
- Example: Key badli to remount
- Follow-up: Index key issue?
- Common wrong answer: 'Virtual DOM hamesha fast hai'

**57. Fiber?**
- Short answer: Work-unit architecture enabling scheduling.

**58. Render vs commit?**
- Short answer: Pure calc vs DOM+effects.
- Detailed: Render component calls (pure), commit DOM apply + effects.
- Example: Effects commit ke baad
- Follow-up: useLayoutEffect kab?
- Common wrong answer: 'Render = DOM update'

**59. Re-render vs DOM update?**
- Short answer: Function run vs actual DOM change.

**60. useLayoutEffect vs useEffect?**
- Short answer: Before paint sync vs after paint.

**61. Concurrent rendering?**
- Short answer: Interruptible rendering with priorities.

**62. useTransition?**
- Short answer: Non-urgent update mark.

**63. Strict Mode double effects?**
- Short answer: Dev check for cleanup/purity.

**64. Why hooks order matters?**
- Short answer: Hooks list index-based.

**65. memo fails why?**
- Short answer: Unstable prop references.

**66. Portal events bubble?**
- Short answer: React tree par bubble.

**67. Compound components?**
- Short answer: Context-shared implicit state composition.

**68. Render props vs hooks?**
- Short answer: Hooks simpler for logic reuse.

**69. Code splitting?**
- Short answer: Dynamic import chunks.

**70. Tree shaking?**
- Short answer: Unused exports removal in build.

**71. Hydration?**
- Short answer: SSR HTML par JS attach.

**72. Redux middleware/thunk?**
- Short answer: Async/side-effects in dispatch pipeline.

**73. Immer?**
- Short answer: Draft mutation -> immutable result.

**74. Selector memoization?**
- Short answer: Derived data recompute avoid.

**75. Race condition fix?**
- Short answer: Abort/ignore stale.

**76. Optimistic update?**
- Short answer: UI pehle update, fail par rollback.

**77. Cookie vs token auth?**
- Short answer: CSRF vs XSS trade-off.

**78. XSS in React?**
- Short answer: dangerouslySetInnerHTML/unsafe URLs.

**79. Virtualization?**
- Short answer: Only visible rows render.

**80. Large app architecture?**
- Short answer: Feature folders, service layer, server-state lib, lazy routes, boundaries.

## Scenario-Based (81-100)

**81. Component 20 baar render ho raha hai?**
- Short answer: Profiler -> cause (parent/context/props/effects) -> colocate state -> memo if measured.
- Detailed: Profile cause -> fix structure -> memo.
- Example: Profiler flame graph
- Follow-up: Context cause?
- Common wrong answer: 'Sab jagah memo lagao'

**82. API 5 sec le rahi hai?**
- Short answer: Skeleton, cache, abort stale, pagination, backend N+1/index, timeout/retry.

**83. Laravel+React auth design?**
- Short answer: Sanctum cookie, /user bootstrap, guards UX, policies.
- Detailed: Sanctum cookie same-site, /user bootstrap, guards UX, policies security.
- Example: login->csrf->session
- Follow-up: Token vs cookie?
- Common wrong answer: 'React route guard se secure ho gaya'

**84. Unnecessary API calls?**
- Short answer: Debounce, cache/dedup, correct deps, abort.

**85. Search lag kar raha hai?**
- Short answer: Debounce, local input state, memo rows, virtualize.

**86. Refresh par logout ho jata hai?**
- Short answer: Auth bootstrap /user missing, state-only auth.

**87. Deploy ke baad refresh 404?**
- Short answer: SPA fallback to index.html.

**88. CORS error?**
- Short answer: Backend origin/credentials config, preflight.

**89. Form double submit?**
- Short answer: Disable on submit + idempotency server.

**90. Stale data after create?**
- Short answer: Invalidate/refetch list.

**91. Memory leak warning?**
- Short answer: Cleanup subscriptions/timers/ObjectURL.

**92. 422 errors UI?**
- Short answer: Map errors by field, nested keys.

**93. Bundle bada hai?**
- Short answer: Analyze, lazy routes, remove heavy libs.

**94. Permissions UI?**
- Short answer: Can() UI, policies API, test 403.

**95. Real-time notifications?**
- Short answer: Polling vs WebSocket/SSE trade-off.

**96. Global state kya use karoge?**
- Short answer: Simplest tool; server state alag.

**97. Table with 50k rows?**
- Short answer: Server pagination or virtualization.

**98. Token expire?**
- Short answer: 401 interceptor -> logout/refresh.

**99. Image upload slow?**
- Short answer: Size limit/compress, progress, direct storage upload.

**100. Legacy class component migrate?**
- Short answer: Incremental, hooks for new, tests first.

