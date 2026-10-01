# Form Libraries: React Hook Form (after native forms)

## 1. Concept (Hinglish)
React Hook Form (RHF) mostly uncontrolled inputs + refs use karta hai, kam re-renders. Validation schema (Zod/Yup) ke saath combine hota hai.

## 2. Why do we need it?
Bade forms me native state boilerplate aur re-renders badh jaate hain.

## 3. Laravel Comparison
FormRequest rules ~ Zod schema (frontend). Dono alag hain, backend authoritative.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual state + errors + touched logic.

## 5. Syntax
```jsx
const { register, handleSubmit, setError, formState: { errors, isSubmitting } } = useForm();
const onSubmit = async (values) => {
  try { await employeeService.create(values); }
  catch (e) {
    const errs = e.response?.data?.errors ?? {};
    Object.entries(errs).forEach(([field, msgs]) => setError(field, { message: msgs[0] }));
  }
};
<form onSubmit={handleSubmit(onSubmit)}>
  <input {...register("name", { required: "Name required" })} />
  {errors.name && <p>{errors.name.message}</p>}
  <button disabled={isSubmitting}>Save</button>
</form>
```
Zod resolver ke liye `@hookform/resolvers` (docs verify).

## 6. Example
Laravel 422 errors ko `setError` se fields par map karna.

## 7. Internal Working
`register` ref + handlers return karta hai; values DOM se read hoti hain, isliye har keystroke pe pura form re-render nahi hota.

## 8. Animation / Flow
```text
register -> input ref -> submit -> validate -> onSubmit -> API -> 422 -> setError
```

## 9. When to use
Medium/large forms.

## 10. When NOT to use
1-2 field form (native kaafi).

## 11. Alternatives
Formik, native state, TanStack Form.

## 12. Why this approach / Trade-offs
Performance + less boilerplate.

## 13. Common Mistakes
Library pehle seekhna (basics miss), backend validation skip.

## 16. Interview Importance
🟡 MEDIUM — Useful

## 17. Interview Questions
- RHF controlled hai ya uncontrolled?
- Server errors kaise dikhate ho?

## 18. Interview English Answer
> React Hook Form relies on uncontrolled inputs and refs, which reduces re-renders, and I combine it with schema validation on the client while mapping Laravel validation errors back with setError.

## 19. Practical Task (solution pehle khud try karo)
Employee form ko RHF + Zod me convert karo.

## 20. Revision Points
- register/handleSubmit
- setError for server errors

