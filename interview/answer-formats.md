# Interview Answer Format: 30-sec / 1-min / Deep / Follow-ups

## useEffect
- **30-sec:** `useEffect` runs side effects after render to sync a component with an external system, re-running when its dependencies change.
- **1-min:** It runs after the DOM is committed. React compares the dependency array with the previous render; if changed it runs cleanup then the effect. I use it for subscriptions, timers and fetches, not for deriving data, which belongs in render.
- **Deep:** Effects are passive and scheduled after paint. Each render has its own closure, so dependencies must include every reactive value used. Strict Mode double-invokes in development to expose missing cleanup. For data fetching I prefer a server-state library to avoid races and manual caching.
- **Follow-ups:** infinite loop causes? race condition fix? effect vs event handler? useLayoutEffect?

## useState vs useReducer vs Context vs Redux
- **30-sec:** Local state -> useState; complex transitions -> useReducer; low-frequency shared value -> Context; large shared client state -> Redux Toolkit.
- **1-min:** I start from the simplest tool and escalate when requirements justify it: lift state for siblings, Context for theme/auth, reducer for related transitions, Redux when many components need selective subscriptions and traceability.
- **Deep:** Context re-renders all consumers on value change, while Redux uses selector subscriptions. Server data belongs in a server-state tool, not in either.
- **Follow-ups:** When NOT Redux? Context perf? Server vs client state?

## Virtual DOM / Reconciliation
- **30-sec:** The virtual DOM is React's in-memory description of the UI; reconciliation diffs old and new trees to update only what changed.
- **1-min:** Render produces a new element tree, React compares it with the previous one using type and key heuristics, then commits minimal DOM changes.
- **Deep:** Fiber splits rendering into units enabling scheduling; render phase is pure, commit applies DOM changes and effects.
- **Follow-ups:** re-render vs DOM update? role of keys? why not index keys?

## Laravel + React Auth
- **30-sec:** Sanctum cookie auth for a same-site SPA, `/user` on load, guards for UX, policies for security.
- **1-min:** CSRF cookie, login sets a session cookie, React hydrates state via `/user`, 401 interceptor logs out, Laravel policies enforce each request.
- **Deep:** Compare cookie (HttpOnly, CSRF needed) vs token (XSS exposure, multi-client), CORS credentials, session regeneration, rate limiting.
- **Follow-ups:** refresh persistence? 401 vs 419? token storage?
