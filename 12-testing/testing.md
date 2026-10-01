# Testing

## 1. Concept (Hinglish)
Unit, component, integration tests. React Testing Library, Vitest/Jest, API mocking, form testing, user interactions.

## 2. Why do we need it?
Refactor safe karne ke liye.

## 3. Laravel Comparison
PHPUnit/Pest feature tests ~ component/integration tests. Farak: React tests user ke nazariye se (UI behavior) likhte hain, implementation details nahi.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual regression.

## 5. Syntax
```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
test("counter increments", async () => {
  render(<Counter />);
  await userEvent.click(screen.getByRole("button", { name: /add/i }));
  expect(screen.getByText("1")).toBeInTheDocument();
});
```

## 6. Example
API ko mock karke loading -> data -> error states test karo (MSW popular option).

## 7. Internal Working
jsdom me component render hota hai, queries role/text se, events simulate.

## 8. Animation / Flow
```text
render -> user action -> assert visible result
```

## 9. When to use
Critical flows, shared components.

## 10. When NOT to use
Implementation details (state values) test karna.

## 11. Alternatives
Cypress/Playwright e2e.

## 12. Why this approach / Trade-offs
User-centric tests refactor ke baad bhi stable.

## 13. Common Mistakes
Implementation test, snapshot spam, act warnings ignore.

## 16. Interview Importance
🟡 MEDIUM — Useful

## 17. Interview Questions
- Unit vs integration?
- RTL philosophy?

## 18. Interview English Answer
> I test components the way users use them: render, interact, and assert on visible output, mocking the network boundary instead of internals.

## 19. Practical Task (solution pehle khud try karo)
Login form test: validation error + success + API fail.

## 20. Revision Points
- Test behavior
- Mock network

