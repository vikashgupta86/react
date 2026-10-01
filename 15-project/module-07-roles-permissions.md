# Module 7: Roles & Permissions

## Requirement
Admin/HR/Employee roles; UI permission-aware; API enforced.

## Laravel
Policies/Gates (ya spatie/laravel-permission). `UserResource` me `permissions` array bhejo.
```php
public function delete(User $user, Employee $employee): bool { return $user->can('employee.delete'); }
```

## React
```jsx
const { can } = useAuth();
{can("employee.delete") && <button onClick={...}>Delete</button>}
<RequireRole roles={["admin"]} />
```

## Key rule
UI hide sirf UX; asli check Laravel policy. Frontend se permission hata ke API test karo (403 aana chahiye).

## Task
Permission-based menu/buttons + API 403 handling UI.

## Interview Qs
- Permissions kahan enforce?
- 401 vs 403?
