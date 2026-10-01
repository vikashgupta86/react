# TypeScript + React

## 1. Concept (Hinglish)
TypeScript JS par static types deta hai: props typing, state typing, events, API response types, generics, utility types.

## 2. Why do we need it?
Compile time pe bugs, better autocomplete, safe refactor.

## 3. Laravel Comparison
PHP type declarations/return types ka similar idea, par TS structural typing hai aur runtime pe erase ho jaati hai (runtime validation nahi deti).

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Runtime bugs, galat props.

## 5. Syntax
```tsx
interface Employee { id: number; name: string; email: string }
type Props = { employee: Employee; onSelect?: (id: number) => void };
function Row({ employee, onSelect }: Props) { ... }
const [list, setList] = useState<Employee[]>([]);
const handle = (e: React.ChangeEvent<HTMLInputElement>) => {};
```

## 6. Example
API response ke liye `ApiResponse<T>` generic.

## 7. Internal Working
Types compile time par check hote hain aur build me hata diye jaate hain. API se aaya data runtime me galat ho to TS nahi pakdega (zod jaisi validation soch sakte ho).

## 8. Animation / Flow
```text
TS code -> type check -> compile to JS (types erased) -> browser
```

## 9. When to use
Medium/large apps, teams.

## 10. When NOT to use
Chhote throwaway scripts (optional).

## 11. Alternatives
JSDoc types, PropTypes (legacy).

## 12. Why this approach / Trade-offs
Market me standard, maintainability.

## 13. Common Mistakes
`any` overuse, assertions (`as`) se errors chhupana.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- interface vs type?
- Generics example?
- TS runtime validation deta hai?

## 18. Interview English Answer
> TypeScript adds compile-time types that are erased at build time, so it improves safety and tooling but does not validate data at runtime.

## 19. Practical Task (solution pehle khud try karo)
Employee types, typed service functions aur typed form state banao.

## 20. Revision Points
- Types compile time
- Avoid any
- API data runtime validate

