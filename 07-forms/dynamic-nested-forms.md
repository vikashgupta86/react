# Dynamic & Nested Forms, Multiple File Upload, Reset

## 1. Concept (Hinglish)
Dynamic fields (add/remove rows), nested objects/arrays in form state, multi-file upload, reset.

## 2. Why do we need it?
HRMS me education/experience/emergency contacts jaise repeating sections.

## 3. Laravel Comparison
Laravel validation `contacts.*.phone` ~ React nested state arrays. Error keys `contacts.0.phone` map karni padti hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Fixed fields.

## 5. Syntax
```jsx
const empty = { name: "", phone: "" };
const [contacts, setContacts] = useState([empty]);
const update = (i, field, value) =>
  setContacts(list => list.map((c, idx) => idx === i ? { ...c, [field]: value } : c));
const add = () => setContacts(list => [...list, { ...empty, id: crypto.randomUUID() }]);
const remove = (i) => setContacts(list => list.filter((_, idx) => idx !== i));
```
Error: Laravel `errors["contacts.0.phone"]`.
Reset: `setForm(initialState)` ya form `key` badal ke remount.

## 6. Example
Rows ke liye stable id key (index nahi) taaki remove par values shift na ho.

## 7. Internal Working
Immutable updates: har level naya array/object banao.

## 8. Animation / Flow
```text
Add click -> new array -> re-render rows -> submit payload array -> Laravel contacts.*.phone validation
```

## 9. When to use
Repeating sections.

## 10. When NOT to use
Bahut complex wizard: form library/state machine.

## 11. Alternatives
React Hook Form `useFieldArray`.

## 12. Why this approach / Trade-offs
Native samajhne ke baad library productivity.

## 13. Common Mistakes
Index keys, nested state mutate, error key mapping.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Dynamic fields me key kya?
- Nested errors map kaise?

## 18. Interview English Answer
> For dynamic rows I keep an array in state, update it immutably, use stable ids as keys, and map Laravel's dotted error keys such as contacts.0.phone back to the right field.

## 19. Practical Task (solution pehle khud try karo)
Emergency contacts add/remove form + Laravel validation errors per row.

## 20. Revision Points
- Stable id keys
- Immutable array updates

