# React Ecosystem, Node, npm, package.json, Vite & Project Structure

## 1. Concept (Hinglish)
**Node.js:** JS ko browser ke bahar chalane wala runtime (build tools ke liye). **npm:** package manager (Laravel ke Composer jaisa). **package.json:** dependencies + scripts (composer.json jaisa). **Vite:** fast dev server + production bundler.

## 2. Why do we need it?
React app bina build tooling ke (JSX compile, bundling, HMR) practical nahi.

## 3. Laravel Comparison
`composer.json` ~ `package.json`; `vendor/` ~ `node_modules/`; `composer.lock` ~ `package-lock.json`; `php artisan serve` ~ `npm run dev`. Laravel Vite plugin Laravel me bhi Vite use karta hai, par yahan React alag SPA hai.

> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

## 4. Without it
Manual script tags, no HMR.

## 5. Syntax
```bash
npm create vite@latest hrms-ui -- --template react
cd hrms-ui && npm install && npm run dev
```
`package.json` scripts: `dev`, `build`, `preview`, `lint`.
```text
src/
  main.jsx       # entry: createRoot().render(<App/>)
  App.jsx
  components/  pages/  hooks/  services/  utils/  assets/
```

## 6. Example
`import.meta.env.VITE_API_URL` se env variable. `.env` me `VITE_API_URL=http://localhost:8000/api`.

## 7. Internal Working
Dev me Vite native ES modules serve karta hai (fast), HMR se changed module replace hota hai. Production me bundle + minify + hashed assets.

## 8. Animation / Flow
```text
npm run dev -> Vite dev server -> browser ES modules + HMR
npm run build -> bundle -> dist/
```

## 9. When to use
Naya SPA project.

## 10. When NOT to use
SEO-heavy site me sirf CRA-style SPA (SSR framework dekho).

## 11. Alternatives
Next.js, Remix, Create React App (ab recommended nahi hai; current docs verify karo).

## 12. Why this approach / Trade-offs
Vite fast aur simple, ecosystem standard.

## 13. Common Mistakes
`node_modules` commit karna, dev dependency vs dependency confusion, exact versions ignore.

## 14. Best Practices
`package-lock.json` commit, ESLint/Prettier, `.env.example`.

## 16. Interview Importance
🟠 HIGH — Frequently Asked

## 17. Interview Questions
- npm install vs npm ci?
- dependencies vs devDependencies?
- Vite kya karta hai?

## 18. Interview English Answer
> Vite is a build tool with a fast dev server using native ES modules and a production bundler. package.json declares dependencies and scripts, similar to composer.json in Laravel.

## 19. Practical Task (solution pehle khud try karo)
Vite se project banao, folder structure setup karo, ek `.env` variable console me print karo.

## 20. Revision Points
- package.json = composer.json
- Vite = dev server + bundler
- VITE_ vars public

