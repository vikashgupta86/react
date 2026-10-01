# Intermediate Interview Questions

1. **useEffect dependency array?** React previous aur current deps compare karta hai (`Object.is`); change par cleanup + effect dobara chalta hai.
2. **Infinite loop in useEffect kab?** Effect state set kare aur wahi state dependency ho, ya object/array dep har render naya ho.
3. **Lifting state up?** Shared state ko nearest common parent me le jana.
4. **Controlled vs uncontrolled?** State vs DOM/ref based value.
5. **Why keys matter?** Reconciliation identity.
6. **useRef vs useState?** Ref re-render trigger nahi karta.
7. **useReducer kab?** Related fields + many transitions.
8. **Context ka downside?** Provider value change par saare consumers re-render.
9. **Stale closure?** Handler purani render ki value capture karta hai; functional update ya correct deps se fix.
10. **Async state updates and batching?** Updates batch hote hain; setState ke baad turant new value nahi milti.
11. **Protected route kaise?** Auth loading handle karke `Navigate`; security Laravel me.
12. **Race condition in fetch?** AbortController / ignore stale responses.

Har question ke liye: definition -> example -> trade-off.
