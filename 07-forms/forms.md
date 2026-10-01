# Forms

## 1. Concept (Hinglish)
Controlled inputs (React state value control karta hai) vs uncontrolled (DOM value, `ref`/FormData). Validation, dynamic fields, file upload, reset, loading, server errors.

## 2. Why do we need it?
Forms har admin app ka core hain.

## 3. Laravel Comparison
Blade form + `old()` + `$errors` ~ React state + errors state. Farak: validation dono jagah: frontend UX ke liye, Laravel FormRequest asli authority.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Page reload based forms.

## 5. Syntax
```jsx
const [form, setForm] = useState({ name: "", email: "" });
const [errors, setErrors] = useState({});
const handleChange = e => setForm(f => ({ ...f, [e.target.name]: e.target.value }));
const handleSubmit = async e => {
  e.preventDefault();
  try { await api.post("/employees", form); }
  catch (err) { setErrors(err.response?.data?.errors ?? {}); }
};
```

## 6. Example
File upload: `const fd = new FormData(); fd.append("avatar", file); api.post("/profile", fd)`.

## 7. Internal Working
Controlled input: render me value state se, `onChange` state update, re-render, input naya value. Har keystroke re-render hota hai (chhote forms me theek).

## 8. Animation / Flow
```text
type -> onChange -> setForm -> render -> input value update
```

## 9. When to use
Controlled: validation/live UI. Uncontrolled: simple/bade forms, file input.

## 10. When NOT to use
Bahut bade forms me har keystroke pe heavy re-render.

## 11. Alternatives
React Hook Form, Formik (pehle native forms samjho).

## 12. Why this approach / Trade-offs
Native forms concepts clear karte hain, phir library productivity deti hai.

## 13. Common Mistakes
Submit double click (loading disable na karna), server errors map na karna, state mutate.

## 14. Best Practices
Loading disable, field-level errors, reusable Input component.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Controlled vs uncontrolled?
- Server validation errors kaise dikhate ho?

## 18. Interview English Answer
> In a controlled input React state is the source of truth for the value. I validate on the client for UX, but always map Laravel's 422 validation errors back to the fields.

## 19. Practical Task (solution pehle khud try karo)
Employee create/edit form: validation, 422 mapping, file upload, loading state.

## 20. Revision Points
- Controlled = state value
- 422 map
- Disable on submit

