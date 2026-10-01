# Laravel + React HRMS Project (Module by Module)

## 1. Concept (Hinglish)
Complete HRMS/Admin dashboard: login, dashboard, role-based access, employee CRUD, search/filter/pagination, details, file upload, profile image, notifications, protected routes, API service layer.

## 2. Why do we need it?
Portfolio aur interview proof.

## 3. Laravel Comparison
Laravel REST API + Sanctum + FormRequest + Resource + Service layer.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 5. Syntax
Modules (ek ek karke, har module me Requirement -> Architecture -> React concepts -> Laravel API -> Flow -> Implementation -> Task -> Code review -> Interview Qs):
1. Setup (Vite + Laravel API + CORS)
2. Auth (login/me/logout)
3. Layout + routing + protected routes
4. Employee list (pagination/search/filter)
5. Employee create/edit (validation + upload)
6. Employee details + delete
7. Roles/permissions UI + API policies
8. Notifications
9. Polish: loading/empty/error, tests, build

## 6. Example
Suggested structure:
```text
src/
  api/ (axios instance)   services/ (employeeService...)
  components/ (ui, shared) features/ (auth, employees)
  hooks/  pages/  routes/  utils/
```

## 7. Internal Working
Har module me end-to-end flow trace karo: UI event -> service -> Laravel -> DB -> response -> state -> UI.

## 9. When to use
Module by module build.

## 10. When NOT to use
Ek saath poora project dump karna.

## 13. Common Mistakes
Pehle UI sab, API baad me; auth/permissions late.

## 14. Best Practices
Chhote vertical slices (UI + API + DB ek feature).

## 16. Interview Importance
🔥 Portfolio + interview proof

## 17. Interview Questions
- Project architecture explain karo.
- Pagination server side kyun?
- Permissions kahan enforce?

## 18. Interview English Answer
> The HRMS app uses a React feature-based structure with a service layer over a Laravel API. Authorization is enforced by Laravel policies while the UI adapts to the user's permissions.

## 19. Practical Task (solution pehle khud try karo)
Module 1 se start karo: Laravel API + React setup, CORS, ek health endpoint se connect.

## 20. Revision Points
- Vertical slices
- Policies backend
- Service layer

