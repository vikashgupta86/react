# Module 1: Setup, CORS, Health Check

## Requirement
React app Laravel API se baat kare. Local dev me CORS aur env sahi ho.

## Architecture
`hrms-ui` (Vite) aur `hrms-api` (Laravel) alag folders.

## React concepts
Vite env, axios instance, `useEffect` + loading/error.

## Laravel API
```php
// routes/api.php
Route::get('/health', fn () => response()->json(['status' => 'ok', 'time' => now()]));
```
`config/cors.php` me `allowed_origins => ['http://localhost:5173']`, `supports_credentials => true`.

## Implementation
```js
// src/services/api.js
import axios from "axios";
export const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,          // http://localhost:8000
  withCredentials: true, withXSRFToken: true,
  headers: { Accept: "application/json" },
});
```
```jsx
function HealthCheck() {
  const [state, setState] = useState({ loading: true });
  useEffect(() => {
    api.get("/api/health").then(r => setState({ data: r.data })).catch(e => setState({ error: e.message }));
  }, []);
  if (state.loading) return <p>Checking...</p>;
  if (state.error) return <p>API down: {state.error}</p>;
  return <p>API: {state.data.status}</p>;
}
```

## Flow
React -> OPTIONS preflight -> Laravel CORS -> GET /api/health -> JSON -> setState -> UI.

## Task
Health page banao; CORS galat karke error dekho aur fix karo.

## Interview Qs
- CORS error aaye to kahan fix?
- Env variables frontend me safe hain?
