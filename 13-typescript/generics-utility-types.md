# TypeScript: Generics, Utility Types, Typing Hooks & API

## 1. Concept (Hinglish)
Generics reusable typed code; utility types (`Partial`, `Pick`, `Omit`, `Record`, `ReturnType`) existing types se naye types.

## 2. Why do we need it?
API responses, form state aur hooks ko type-safe banane ke liye.

## 3. Laravel Comparison
PHP generics nahi hain (docblocks `@template`). TS generics runtime pe erase hote hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
`any` everywhere.

## 5. Syntax
```ts
interface Paginated<T> { data: T[]; meta: { current_page: number; last_page: number; total: number } }
type EmployeeForm = Omit<Employee, "id" | "avatar_url">;
type EmployeeUpdate = Partial<EmployeeForm>;
async function get<T>(url: string): Promise<T> { return (await api.get<T>(url)).data; }
const list = await get<Paginated<Employee>>("/employees");
function useLocalStorage<T>(key: string, initial: T) { const [v, setV] = useState<T>(initial); return [v, setV] as const; }
const [count, setCount] = useState<number | null>(null);
const handle = (e: React.FormEvent<HTMLFormElement>) => {};
```

## 6. Example
Props: `type ButtonProps = React.ComponentProps<"button"> & { variant?: "primary" | "ghost" }`.

## 7. Internal Working
Structural typing: shape match ho to compatible. Types build me erase.

## 8. Animation / Flow
```text
type check (compile) -> JS emit -> runtime (no types)
```

## 9. When to use
Medium/large codebase.

## 10. When NOT to use
`any`/`as` se errors chhupana.

## 11. Alternatives
Zod schema + `z.infer` (runtime + types).

## 12. Why this approach / Trade-offs
Refactor safety + autocomplete.

## 13. Common Mistakes
`any`, wrong assertions, API runtime shape vs type mismatch.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- interface vs type?
- Generic example?
- Partial/Pick/Omit?
- TS runtime validation?

## 18. Interview English Answer
> Generics let me write reusable typed code like a Paginated<T> response, and utility types derive new types from existing ones. Types disappear at runtime, so external data still needs validation.

## 19. Practical Task (solution pehle khud try karo)
Employee types, `Paginated<T>`, typed service + typed `useEmployees` hook.

## 20. Revision Points
- Generics
- Utility types
- Types erased

