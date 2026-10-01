# Module 9: Polish, Tests & Production Build

## Checklist
- Loading/empty/error states har screen par
- Error boundary route level
- Accessibility (labels, focus, keyboard)
- Tests: login, employee form (422), permission UI
- `npm run build`, env production, SPA fallback
- Security checklist (see `14-production/security-deep.md`)

```nginx
location / { try_files $uri /index.html; }
```

## Task
Final audit: Lighthouse, bundle analysis, 3 RTL tests, deploy.

## Interview Qs
- Project architecture explain karo.
- Aap performance kaise improve karoge?
