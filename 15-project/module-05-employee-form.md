# Module 5: Create / Edit Employee (validation + upload)

## Requirement
Create/edit form, validation errors, avatar upload with preview, loading state.

## React concepts
Controlled form, FormData, mutation, error mapping, `useEffect` prefill (edit).

## Laravel API
`POST /api/employees` (FormRequest), update via `POST /api/employees/{id}` with `_method=PUT` for multipart.

## Implementation
```jsx
function EmployeeForm({ initial, onSubmit }) {
  const [form, setForm] = useState(initial ?? { name: "", email: "", department_id: "" });
  const [file, setFile] = useState(null);
  const [errors, setErrors] = useState({});
  const [saving, setSaving] = useState(false);
  const preview = useMemo(() => (file ? URL.createObjectURL(file) : initial?.avatar_url), [file, initial]);
  useEffect(() => () => { if (file) URL.revokeObjectURL(preview); }, [file, preview]);

  const submit = async (e) => {
    e.preventDefault(); setSaving(true); setErrors({});
    const fd = new FormData();
    Object.entries(form).forEach(([k, v]) => fd.append(k, v));
    if (file) fd.append("avatar", file);
    try { await onSubmit(fd); }
    catch (err) { setErrors(err.response?.data?.errors ?? {}); }
    finally { setSaving(false); }
  };
  ...
}
```

## Flow
Submit -> FormData -> multipart -> FormRequest -> store -> JSON -> invalidate list -> navigate.

## Task
Create + edit form, 422 errors per field, avatar preview.

## Interview Qs
- Multipart me PUT issue?
- ObjectURL cleanup kyun?
