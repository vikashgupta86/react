# HRMS Project: Overview & Build Order

**Stack:** Laravel (API + Sanctum + MySQL) + React (Vite) + Axios + React Router (+ React Query).

```text
React pages -> features -> hooks -> services -> axios
        | HTTPS JSON + Sanctum cookie
Laravel: Route -> Middleware -> FormRequest -> Controller -> Service -> Model -> MySQL
```

## Modules (ek ek karke banao)
1. Setup & CORS
2. Authentication
3. Layout, Routing & Guards
4. Employee List (search/filter/sort/paginate)
5. Employee Create/Edit (validation + upload)
6. Employee Details & Delete
7. Roles & Permissions
8. Notifications
9. Polish, Tests & Build

## Har module ka format
Requirement -> Architecture -> React concepts -> Laravel API -> Flow -> Implementation -> Task -> Code Review -> Interview Qs

**Rule:** Task ka solution khud likho, phir review ke liye bhejo. Ye files reference implementation hain, copy-paste se seekhna nahi hota.
