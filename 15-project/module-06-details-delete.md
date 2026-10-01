# Module 6: Details & Delete

## Requirement
Employee detail page (`/employees/:id`), delete with confirmation, 404 handling.

## Implementation
```jsx
const { id } = useParams();
const { data, isPending, error } = useQuery({ queryKey: ["employee", id], queryFn: () => employeeService.get(id) });
if (error?.response?.status === 404) return <NotFound />;

const qc = useQueryClient();
const del = useMutation({
  mutationFn: () => employeeService.remove(id),
  onSuccess: () => { qc.invalidateQueries({ queryKey: ["employees"] }); navigate("/employees"); },
});
```
Laravel: `DELETE /api/employees/{id}` with `$this->authorize('delete', $employee)`.

## Task
Detail page, delete confirm modal (Portal), 404 handling, success toast.

## Interview Qs
- Optimistic update kab?
- 403 vs 404 UI?
