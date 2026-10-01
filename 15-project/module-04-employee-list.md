# Module 4: Employee List

## Requirement
Table with search, department filter, sort, server pagination, 4 states.

## Laravel API
`GET /api/employees?page=&search=&department_id=&sort=&direction=` (see `05-api-integration/laravel-api-code.md`).

## Implementation (React Query version)
```jsx
function EmployeesPage() {
  const [params, setParams] = useSearchParams();
  const page = Number(params.get("page") ?? 1);
  const search = params.get("search") ?? "";
  const debounced = useDebounce(search, 400);

  const { data, isPending, isError, refetch } = useQuery({
    queryKey: ["employees", { page, search: debounced }],
    queryFn: () => employeeService.list({ page, search: debounced }),
    placeholderData: keepPreviousData,
  });

  if (isPending) return <Skeleton />;
  if (isError) return <ErrorState onRetry={refetch} />;
  if (!data.data.length) return <EmptyState text="No employees found" />;
  return (<>
    <SearchBox value={search} onChange={v => setParams({ search: v, page: 1 })} />
    <EmployeeTable rows={data.data} />
    <Pagination page={page} last={data.meta.last_page} onChange={p => setParams({ search, page: p })} />
  </>);
}
```

## Flow
Type -> debounce -> params -> queryKey change -> request -> render.

## Task
Table + search + filter + sort + pagination, URL params se.

## Interview Qs
- Debounce kyun? Stale response kaise handle?
- Server vs client pagination?
