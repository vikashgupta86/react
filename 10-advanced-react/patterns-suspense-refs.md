# Compound Components, forwardRef, Suspense, Portals, Error Boundaries

## 1. Concept (Hinglish)
Compound components: related components implicit shared state ke saath (`<Tabs><Tabs.Tab/></Tabs>`). `forwardRef`/ref as prop: parent ko child ke DOM node tak ref dena. Suspense: loading boundary. Portal: DOM me alag jagah render.

## 2. Why do we need it?
Reusable, flexible UI libraries (Modal, Tabs, Dropdown) banane ke liye.

## 3. Laravel Comparison
Blade slots/components composition jaisa idea.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Props ka explosion (`showHeader`, `showFooter`...).

## 5. Syntax
```jsx
const TabsContext = createContext();
function Tabs({ children, defaultValue }) {
  const [active, setActive] = useState(defaultValue);
  return <TabsContext.Provider value={{ active, setActive }}>{children}</TabsContext.Provider>;
}
Tabs.Tab = function Tab({ value, children }) {
  const { active, setActive } = useContext(TabsContext);
  return <button aria-selected={active === value} onClick={() => setActive(value)}>{children}</button>;
};
// Portal
createPortal(<div className="modal">...</div>, document.body);
// Suspense + lazy
<Suspense fallback={<Spinner/>}><LazyPage/></Suspense>
```
`forwardRef` ya newer React me ref as prop: version ke hisaab se docs verify karo.

## 6. Example
Modal Portal se body me render hota hai taaki CSS stacking/overflow issues na aayein.

## 7. Internal Working
Portal React tree me parent ka child rehta hai (events bubble hote hain) par DOM me alag node me. Suspense child ke promise/lazy load hone tak fallback dikhata hai.

## 8. Animation / Flow
```text
lazy component render -> chunk loading -> Suspense fallback -> chunk ready -> real UI
```

## 9. When to use
Design-system components.

## 10. When NOT to use
Simple pages me over-engineering.

## 11. Alternatives
Render props, config props, headless libraries (Radix).

## 12. Why this approach / Trade-offs
Flexible API, kam props.

## 13. Common Mistakes
Context ke bina implicit state, portal accessibility (focus trap) bhoolna.

## 16. Interview Importance
🟡 MEDIUM — Useful (Suspense/lazy 🟠)

## 17. Interview Questions
- Compound components kya?
- Portal kab?
- Error boundary kya catch nahi karta?

## 18. Interview English Answer
> Compound components share implicit state through context so consumers compose flexible UIs with a small API. Portals render children into another DOM node while keeping React tree behavior such as event bubbling.

## 19. Practical Task (solution pehle khud try karo)
Tabs compound component + Modal Portal (ESC close, focus) banao.

## 20. Revision Points
- Compound = context + composition
- Portal DOM alag, React tree same

