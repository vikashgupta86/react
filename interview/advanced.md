# Advanced Interview Questions

1. **Reconciliation kaise kaam karta hai?** Same type update, alag type replace, list me key matching.
2. **Fiber kya hai?** React ka internal work-unit architecture jo rendering ko scheduling/priority ke saath possible banata hai.
3. **Render vs commit?** Render pure calculation; commit DOM apply + effects.
4. **Re-render vs DOM update?** Re-render me function chalta hai; DOM sirf changed parts update hote hain.
5. **useMemo/useCallback kab nahi?** Jab measured benefit na ho; memo khud cost hai.
6. **React.memo kyun fail hota hai?** Props me naye object/function references.
7. **Concurrent features (Suspense, transitions)?** Latest React docs se verify karke batao.
8. **Large app architecture?** Feature-based folders, service layer, server-state tool, route-level code splitting, error boundaries.
9. **Server state vs client state?** Server state remote/stale/cached hai.
10. **Cookie vs token auth trade-offs?** CSRF vs XSS risk, same-site vs cross-client.
