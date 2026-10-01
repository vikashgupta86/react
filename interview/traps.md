# React Interview Traps

| Topic | Common wrong answer | Better answer |
|---|---|---|
| State vs Props | "Dono data hain" | Props read-only inputs, state owned data jo re-render trigger karta hai |
| useEffect | "componentDidMount jaisa" | External system sync; deps ke basis par re-sync |
| Dependency array | "Sirf performance ke liye" | Correctness: effect jin reactive values use karta hai wo deps me |
| useMemo vs useCallback | "Same hain" | Value cache vs function reference cache |
| Controlled/uncontrolled | "Controlled slow hota hai" | Control ka source alag: state vs DOM |
| Virtual DOM | "Faster than DOM" | Declarative updates ke liye abstraction; diffing se minimal DOM changes |
| Keys | "Warning hatane ke liye" | Identity for reconciliation/state |
| Closures/stale state | "React bug hai" | Render snapshot + closure; functional update/deps |
| Async setState | "setState async hai" | Updates scheduled/batched; value next render me |
| Re-render vs DOM update | "Same" | Re-render function call; DOM sirf diff ke baad |
| Context | "Redux replacement" | Value sharing; frequent updates par re-render cost |
| Redux | "Always best" | Large complex client state ke liye, har jagah nahi |
| Server vs client state | "Sab Redux me" | Server state cached/stale; dedicated tool |
