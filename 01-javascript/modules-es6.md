# Modules (import/export) & ES6+ Features

## 1. Concept (Hinglish)
ES Modules code ko files me baantte hain. `export` se bahar dena, `import` se lena. ES6+ me: template literals, default params, destructuring, spread/rest, optional chaining, `??`, classes, `Array` methods, `Object.entries`, `Promise`, `async/await`.

## 2. Why do we need it?
React project me har component ek module hai. Vite/bundler modules ko jodta hai (tree shaking, code splitting, lazy import).

## 3. Laravel Comparison
PHP `namespace`/`use` + Composer autoload ~ JS `import/export` + bundler. Farak: JS me import explicit path se hota hai aur static analysis se unused code hataya ja sakta hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Global scripts, `<script>` tags ka order dependency.

## 5. Syntax
```js
// math.js
export const add = (a, b) => a + b;     // named
export default function multiply(a, b) { return a * b; }  // default
// app.js
import multiply, { add } from "./math.js";
const Lazy = () => import("./Heavy.js");  // dynamic import
```

## 6. Example
```jsx
import { useState } from "react";
import Button from "./components/Button";
export default function App() {}
```

## 7. Internal Working
Modules strict mode me chalte hain, apna scope hota hai, ek baar evaluate hote hain (cache). Bundler dependency graph banata hai. Dynamic `import()` alag chunk banata hai jo runtime pe load hota hai.

## 8. Animation / Flow
```text
main.jsx -> imports -> dependency graph -> bundler -> chunks -> browser load
```

## 9. When to use
Har file ek responsibility. Named exports utilities ke liye, default export component ke liye (team convention).

## 10. When NOT to use
Circular imports; barrel files (`index.js` re-export) jab bade app me tree shaking/slow startup issue de.

## 11. Alternatives
CommonJS (`require`) legacy/Node.

## 12. Why this approach / Trade-offs
Static structure -> better tooling aur optimization.

## 13. Common Mistakes
Default vs named import mix-up, circular dependency, file extension/case issues.

## 14. Best Practices
Absolute alias imports (`@/`), ek component ek file, circular imports avoid.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- Named vs default export?
- Dynamic import kya hai, React me kahan?
- ES modules vs CommonJS?

## 18. Interview English Answer
> ES modules provide file-level scope with explicit imports and exports. Because they are statically analyzable, bundlers can tree-shake unused code and split dynamic imports into separate chunks.

## 19. Practical Task (solution pehle khud try karo)
Utility module banao (named exports) aur ek component default export karo; ek heavy component ko dynamic import se lazy load karo.

## 20. Revision Points
- export/import
- default vs named
- dynamic import = code splitting

