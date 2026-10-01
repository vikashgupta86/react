# Pagination, Search, Filtering, Sorting (React side)

## 1. Concept (Hinglish)
Server-side pagination: React page/search/filter/sort params API ko bhejta hai, API chhota page deta hai.

## 2. Why do we need it?
10,000 rows ek saath fetch karna slow aur wasteful hai.

## 3. Laravel Comparison
`paginate()` + query params + `when()` filters ka client side. URL query params (`?page=2`) state ka source ban sakte hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Poora data load karke client me filter (bade data par slow).

## 5. Syntax
```jsx
function EmployeesPage() {
  const [params, setParams] = useSearchParams();
  const page = Number(params.get("page") ?? 1);
  const search = params.get("search") ?? "";
  const debounced = useDebounce(search, 400);
  const { data, loading } = useEmployees({ page, search: debounced });

  const onSearch = (v) => setParams({ search: v, page: 1 }); // search badle to page 1
  return (<>
    <input value={search} onChange={e => onSearch(e.target.value)} />
    <Table rows={data?.data} />
    <Pagination page={page} last={data?.meta.last_page}
      onChange={p => setParams({ search, page: p })} />
  </>);
}
```

## 6. Example
URL me params hone se refresh/bookmark/share par same view milta hai.

## 7. Internal Working
Debounce: typing ruke tab hi API call. Param change -> effect/query re-run -> naya page.

## 8. Animation / Flow
```text
type -> debounce 400ms -> params change -> request -> meta.last_page -> pagination UI
```

## 9. When to use
Bade datasets.

## 10. When NOT to use
Chhoti static list (client filter chalega).

## 11. Alternatives
Infinite scroll, cursor pagination (`cursorPaginate`), virtualization.

## 12. Why this approach / Trade-offs
URL state + server pagination scalable aur shareable.

## 13. Common Mistakes
Search badalne par page reset na karna, har keystroke pe call, stale response overwrite.

## 14. Best Practices
Debounce + abort stale + page reset.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Offset vs cursor pagination?
- Debounce kyun?
- Filters URL me kyun?

## 18. Interview English Answer
> I drive list screens from URL query parameters, debounce search input, reset to page one on filter changes, and let the Laravel API paginate so the client only loads what it shows.

## 19. Practical Task (solution pehle khud try karo)
Employees table: search, department filter, sortable columns, pagination, sab URL params se.

## 20. Revision Points
- Server-side pagination
- Debounce
- Page reset

