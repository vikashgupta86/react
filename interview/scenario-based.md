# Scenario Based Questions

## 1. Component 20 baar render ho raha hai
1. React DevTools Profiler se confirm karo kya render hua aur kyun.
2. Parent state/Context change, unstable props, effect loops check karo.
3. State neeche le jao (colocation), phir memo/useCallback jahan measured benefit ho.

## 2. API 5 seconds le rahi hai
Skeleton/loading, cancel stale requests, caching (React Query), pagination, backend optimize (N+1, index), timeout + retry + error UI.

## 3. Laravel + React authentication design
Sanctum SPA cookie (same-site) ya token (multi-client). `/user` bootstrap, 401 interceptor, route guards UX ke liye, policies backend me.

## 4. Large React app ka architecture
Feature-based structure, API/service layer, shared UI components, server-state library, lazy routes, error boundaries, testing strategy, TypeScript.

## 5. Unnecessary API calls kaise rokoge
Debounce search, AbortController, caching/dedup (React Query), proper dependency array, avoid effect chains.

## 6. Search box har keystroke pe lag kar raha
Debounce, input state ko locally rakho, list virtualize/paginate, memoized rows.

Har answer ka format: **Problem -> Diagnose -> Options -> Choice + Why -> Trade-off**.
