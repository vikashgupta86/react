# React + Laravel API Integration

## 1. Concept (Hinglish)
React Axios/fetch se Laravel REST API ko call karta hai, JSON me data lata hai. Topics: GET/POST/PUT/PATCH/DELETE, headers, auth, CORS, CSRF, validation errors (422), pagination, search/filter/sort, file upload, download.

## 2. Why do we need it?
Frontend aur backend alag apps hain, sirf HTTP/JSON se baat karte hain.

## 3. Laravel Comparison
Tumhara Laravel API knowledge yahan seedha kaam aata hai (routes, controllers, resources, validation). Farak: Blade me data direct view me jaata tha, ab API contract (JSON shape, status codes) design karna padta hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Server-rendered forms, full reload.

## 5. Syntax
```js
// services/api.js
import axios from "axios";
export const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,
  withCredentials: true,     // cookie based Sanctum SPA auth
  headers: { Accept: "application/json" },
});
// services/employeeService.js
export const getEmployees = (params) => api.get("/employees", { params }).then(r => r.data);
```
Laravel: `Route::apiResource('employees', EmployeeController::class)`, `EmployeeResource`, `FormRequest` validation.

## 6. Example
```jsx
try {
  await api.post("/employees", form);
} catch (e) {
  if (e.response?.status === 422) setErrors(e.response.data.errors); // Laravel validation format
}
```
File upload: `FormData` + `multipart/form-data`, Laravel me `$request->file('avatar')`.

## 7. Internal Working
Request flow: React event -> service function -> Axios -> browser HTTP request -> (CORS preflight agar cross-origin) -> Laravel middleware -> route -> FormRequest -> controller -> service -> model -> DB -> JSON Resource -> response -> Axios promise resolve -> state update -> render.

## 8. Animation / Flow
```text
Click -> handler -> service -> axios -> HTTP -> Laravel route -> middleware -> controller -> DB
-> JSON response -> then/await -> setState -> render
```

## 9. When to use
Service layer me saari API calls, interceptors me common error/auth handling.

## 10. When NOT to use
Components me direct scattered axios calls (maintenance mushkil).

## 11. Alternatives
fetch, React Query/SWR (server-state), RTK Query.

## 12. Why this approach / Trade-offs
Service layer + axios instance: ek jagah base URL, headers, interceptors.

## 13. Common Mistakes
CORS ko frontend se fix karne ki koshish (backend config hai), 422 errors ignore, loading/error state bhoolna, pagination server side na karna, token localStorage pe bina XSS soche.

## 14. Best Practices
Env based baseURL, consistent error format, abort stale requests, pagination server side, debounce search.

## 15. Wrong vs Better Approach
```jsx
// Wrong: component me hardcoded URL
axios.get("http://localhost:8000/api/users")
// Better: service + env baseURL
```

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- CORS kya hai aur Laravel me kaise configure?
- 401 vs 403 vs 422?
- Cookie auth vs token auth?
- Unnecessary API calls kaise rokoge?

## 18. Interview English Answer
> I isolate API calls in a service layer built on a configured Axios instance. The backend returns consistent JSON and status codes, and the UI handles loading, error and validation (422) states explicitly.

## 19. Practical Task (solution pehle khud try karo)
Employees list API (pagination + search) Laravel me banao aur React table me integrate karo, loading/empty/error ke saath.

## 20. Revision Points
- Service layer
- 422 = validation errors
- CORS backend config
- Server-side pagination

