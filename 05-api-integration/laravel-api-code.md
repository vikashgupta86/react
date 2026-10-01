# Laravel API Side: Employees API (Route -> Controller -> Service -> Model)

## 1. Concept (Hinglish)
React ko jo API chahiye uska Laravel backend: `apiResource`, FormRequest validation, Resource (JSON shape), Service layer, pagination.

## 2. Why do we need it?
React tab tak integrate nahi ho sakta jab tak API contract clear na ho.

## 3. Laravel Comparison
Ye tumhara home ground hai. Naya sirf ye: response JSON contract frontend ke liye consistent rakhna.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Blade views return karna.

## 5. Syntax
```php
// routes/api.php
Route::middleware('auth:sanctum')->group(function () {
    Route::apiResource('employees', EmployeeController::class);
});

// app/Http/Requests/StoreEmployeeRequest.php
public function rules(): array {
    return [
        'name' => ['required', 'string', 'max:100'],
        'email' => ['required', 'email', 'unique:employees,email'],
        'department_id' => ['required', 'exists:departments,id'],
        'avatar' => ['nullable', 'image', 'max:2048'],
    ];
}

// app/Http/Resources/EmployeeResource.php
public function toArray($request): array {
    return [
        'id' => $this->id, 'name' => $this->name, 'email' => $this->email,
        'department' => $this->department?->name,
        'avatar_url' => $this->avatar ? asset('storage/'.$this->avatar) : null,
    ];
}

// app/Http/Controllers/EmployeeController.php
public function index(Request $request, EmployeeService $service) {
    return EmployeeResource::collection($service->paginate($request->only(['search','department_id','sort','direction','per_page'])));
}
public function store(StoreEmployeeRequest $request, EmployeeService $service) {
    return new EmployeeResource($service->create($request->validated()));
}

// app/Services/EmployeeService.php
public function paginate(array $f) {
    return Employee::query()->with('department')
        ->when($f['search'] ?? null, fn($q, $s) => $q->where(fn($q) => $q->where('name','like',"%$s%")->orWhere('email','like',"%$s%")))
        ->when($f['department_id'] ?? null, fn($q, $d) => $q->where('department_id', $d))
        ->orderBy(in_array($f['sort'] ?? '', ['name','created_at']) ? $f['sort'] : 'created_at',
                  ($f['direction'] ?? 'desc') === 'asc' ? 'asc' : 'desc')
        ->paginate(min((int)($f['per_page'] ?? 10), 100));
}
```
Validation fail par Laravel API request me `Accept: application/json` ho to automatic **422** deta hai: `{ message, errors: { field: [..] } }`.

## 6. Example
`EmployeeResource::collection(paginator)` response: `{ data: [...], links: {...}, meta: { current_page, last_page, per_page, total, ... } }`.

## 7. Internal Working
Request -> middleware (auth:sanctum) -> route -> FormRequest validate -> controller -> service -> Eloquent -> DB -> Resource transform -> JSON.

## 8. Animation / Flow
```text
GET /api/employees?page=2&search=ra -> middleware -> controller -> service query -> paginate -> Resource -> JSON
```

## 9. When to use
Har resource ke liye Resource + FormRequest.

## 10. When NOT to use
Controller me bhari business logic.

## 11. Alternatives
Fractal/other transformers, GraphQL.

## 12. Why this approach / Trade-offs
Resource se API contract stable, model changes frontend na todein.

## 13. Common Mistakes
N+1 (`with()` bhoolna), sort column whitelist na karna (SQL risk), per_page unlimited.

## 14. Best Practices
Whitelist sort fields, cap per_page, `with()`, consistent errors.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- 422 response ka format?
- Pagination meta kya deta hai?
- N+1 kaise rokte ho?

## 18. Interview English Answer
> I expose a resource-based REST API with FormRequest validation, API Resources for a stable JSON shape and server-side pagination, with the query logic in a service so controllers stay thin.

## 19. Practical Task (solution pehle khud try karo)
Employees API banao: list (search+filter+sort+paginate), store, update, destroy, ek test curl/Postman se verify karo.

## 20. Revision Points
- apiResource + FormRequest + Resource
- Whitelist sort
- Cap per_page

