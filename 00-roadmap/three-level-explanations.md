# Difficult Topics: 3 Levels

## useEffect
- **Level 1:** Render ke baad bahar ka kuch kaam karna ho (API, timer) to effect.
- **Level 2:** Dependencies badle to effect dobara; cleanup pehle chalta hai; deps me wo sab values jo effect use karta hai.
- **Level 3:** Render/commit ke baad passive effects schedule hote hain; React deps ko `Object.is` se compare karta hai; Strict Mode dev me extra mount/unmount se cleanup bugs pakadta hai.

## Closure / stale state
- **L1:** Function apni purani values yaad rakhta hai.
- **L2:** Har render ka handler us render ki state capture karta hai; functional update se fix.
- **L3:** Lexical environment function ke saath attach; hooks closures + per-render snapshot model.

## Reconciliation
- **L1:** React purana aur naya UI compare karke sirf badla hua hissa update karta hai.
- **L2:** Same type update, alag type replace, list me key se match.
- **L3:** Fiber work-in-progress tree, render phase pure/interruptible, commit phase DOM mutate.

## Context
- **L1:** Data sabko bina har level pass kiye.
- **L2:** Provider value change -> sab consumers re-render.
- **L3:** Context consumers dependency track hoti hai provider value identity se; selective subscription nahi.

## Server state
- **L1:** Server ka data jo hum copy karke rakhte hain.
- **L2:** Stale ho sakta hai, cache/invalidate/refetch chahiye.
- **L3:** Query key identity, dedup, background refetch, garbage collection time.
