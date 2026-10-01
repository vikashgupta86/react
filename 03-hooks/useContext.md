# useContext

## 1. Concept (Hinglish)
Context data ko component tree me bina har level pe props pass kiye share karta hai.

## 2. Why do we need it?
Prop drilling avoid karne ke liye (theme, auth user, language).

## 3. Laravel Comparison
Blade me `View::share()` / global shared data ka idea similar. Farak: Context change hone par consumers re-render hote hain.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Deep prop drilling.

## 5. Syntax
```jsx
const ThemeContext = createContext("light");
<ThemeContext.Provider value={theme}><App/></ThemeContext.Provider>
const theme = useContext(ThemeContext);
```

## 6. Example
AuthContext: `{user, login, logout}`.

## 7. Internal Working
Provider ka `value` badalte hi us context ke saare consumers re-render hote hain. `value={{...}}` har render naya object banata hai, isliye memoize karo ya split contexts.

## 8. Animation / Flow
```text
Provider value change -> saare consumers re-render
```

## 9. When to use
Kam-frequency update wali shared values (theme, auth, locale).

## 10. When NOT to use
Frequently changing bada state, complex logic.

## 11. Alternatives
Props, composition, Redux Toolkit, Zustand.

## 12. Why this approach / Trade-offs
Built-in, simple, par fine-grained subscription nahi deta.

## 13. Common Mistakes
Ek giant context, object value har render naya, sab kuch context me.

## 16. Interview Importance
🔥 VERY HIGH — Must Know

## 17. Interview Questions
- Context vs Redux?
- Context perf issue?

## 18. Interview English Answer
> Context lets a value be shared across a component subtree without prop drilling. All consumers re-render when the provider value changes, so it suits low-frequency data.

## 19. Practical Task (solution pehle khud try karo)
ThemeContext aur AuthContext banao, value memoize karo.

## 20. Revision Points
- Context = shared value
- Value change = consumers re-render

