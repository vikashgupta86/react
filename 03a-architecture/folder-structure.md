# Component Architecture & Industry Folder Structure

## 1. Concept (Hinglish)
Large React app ko maintainable rakhne ke liye separation of concerns: UI components, pages, feature modules, hooks, services (API), utils, constants.

## 2. Why do we need it?
Project bada hone par "sab components folder me" structure chaos ban jaata hai.

## 3. Laravel Comparison
Laravel me Controller/Service/Model/Request/Resource separation hota hai. React me similar idea: page (controller-ish), component (view), service (API), hook (logic).

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Giant components jisme UI + API + logic sab.

## 5. Syntax
Feature-based structure:
```text
src/
  app/            # router, providers, store
  components/ui/  # Button, Input, Modal (generic)
  features/
    auth/         # LoginForm, useAuth, authService
    employees/    # EmployeeTable, EmployeeForm, useEmployees, employeeService
  hooks/          # generic hooks (useDebounce)
  services/       # axios instance, interceptors
  utils/  constants/  types/
  pages/          # route-level screens
```

## 6. Example
`EmployeesPage` -> `useEmployees` hook -> `employeeService.getAll()` -> axios -> Laravel.

## 7. Internal Working
Dependency direction: pages -> features -> components/ui -> utils. UI components API ya router se coupled na hon (reusable rahein).

## 8. Animation / Flow
```text
Page -> Feature component -> custom hook -> service -> API
```

## 9. When to use
Medium/large apps.

## 10. When NOT to use
Chhote demo app me over-engineering.

## 11. Alternatives
Type-based (components/hooks/services), feature-based, Atomic design.

## 12. Why this approach / Trade-offs
Feature-based me ek feature ka sab kuch ek jagah, delete/modify aasan.

## 13. Common Mistakes
Components me direct axios, utils me bahut logic, circular imports, har cheez global.

## 14. Best Practices
Chhote components, service layer, consistent naming, barrel files soch samajh ke.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Large React app ka structure kaise?
- Service layer kyun?
- Presentational vs container components?

## 18. Interview English Answer
> I organize by feature, keep generic UI components separate, and put API access in a service layer behind custom hooks, so components focus on rendering and stay reusable.

## 19. Practical Task (solution pehle khud try karo)
HRMS ke liye folder structure banao aur `employees` feature ke files likho (empty bhi chalega).

## 20. Revision Points
- Feature-based
- Service layer
- Dependency direction

