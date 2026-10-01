# Module 2: Authentication

## Requirement
Login, logout, current user, session persist on refresh.

## Architecture
`features/auth`: `authService`, `AuthProvider`, `useAuth`, `LoginPage`.

## React concepts
Context, effect on mount, loading state, 422 error mapping.

## Laravel API
Sanctum SPA setup (see `06-authentication/auth-full-build.md`): `/sanctum/csrf-cookie`, `/login`, `/logout`, `/api/user`.

## Implementation (Login page)
```jsx
function LoginPage() {
  const { login } = useAuth();
  const navigate = useNavigate();
  const location = useLocation();
  const [form, setForm] = useState({ email: "", password: "" });
  const [errors, setErrors] = useState({});
  const [submitting, setSubmitting] = useState(false);

  const onSubmit = async (e) => {
    e.preventDefault(); setSubmitting(true); setErrors({});
    try { await login(form); navigate(location.state?.from?.pathname ?? "/", { replace: true }); }
    catch (err) { setErrors(err.response?.data?.errors ?? { email: ["Login failed"] }); }
    finally { setSubmitting(false); }
  };
  return (
    <form onSubmit={onSubmit}>
      <input value={form.email} onChange={e => setForm(f => ({ ...f, email: e.target.value }))} />
      {errors.email && <p>{errors.email[0]}</p>}
      <input type="password" value={form.password} onChange={e => setForm(f => ({ ...f, password: e.target.value }))} />
      <button disabled={submitting}>Login</button>
    </form>
  );
}
```

## Flow
Submit -> csrf cookie -> POST /login -> session cookie -> setUser -> redirect.

## Task
Login/logout aur refresh pe user persist. Wrong password par error dikhao.

## Interview Qs
- Refresh par user kaise milta hai?
- 401 aur 419 me farak?
