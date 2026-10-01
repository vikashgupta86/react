# Testing: API Mocking, Forms, Interactions, Integration

## 1. Concept (Hinglish)
Network boundary mock karo (MSW ya vi.mock), user interactions simulate karo, async UI assert karo.

## 2. Why do we need it?
Real API par tests slow/flaky hote hain.

## 3. Laravel Comparison
`Http::fake()` ~ MSW/vi.mock. Feature test ~ integration test.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual testing har change par.

## 5. Syntax
```jsx
// Vitest + RTL
test("shows validation error from API", async () => {
  server.use(http.post("/api/employees", () => HttpResponse.json({ errors: { email: ["Taken"] } }, { status: 422 })));
  render(<EmployeeForm />);
  await userEvent.type(screen.getByLabelText(/email/i), "a@b.com");
  await userEvent.click(screen.getByRole("button", { name: /save/i }));
  expect(await screen.findByText("Taken")).toBeInTheDocument();
});
```
MSW API version ke hisaab se badli hai (v2 `http`/`HttpResponse`), docs verify karo.

## 6. Example
Loading -> data -> error: `findBy*` (async), `queryBy*` (absence).

## 7. Internal Working
jsdom me render, queries accessibility-based.

## 8. Animation / Flow
```text
mock API -> render -> user event -> await UI -> assert
```

## 9. When to use
Forms, auth flows, critical paths.

## 10. When NOT to use
Implementation details/snapshot spam.

## 11. Alternatives
Playwright/Cypress e2e.

## 12. Why this approach / Trade-offs
User-behavior tests refactor-safe.

## 13. Common Mistakes
getBy for async, act warnings ignore, testing state internals.

## 16. Interview Importance
🟡 MEDIUM — Useful

## 17. Interview Questions
- getBy vs findBy vs queryBy?
- API kaise mock karte ho?

## 18. Interview English Answer
> I test behavior through the UI with Testing Library and mock only the network boundary, using findBy queries for async results.

## 19. Practical Task (solution pehle khud try karo)
Login form test: validation, success redirect, API 401.

## 20. Revision Points
- findBy async
- Mock network only

