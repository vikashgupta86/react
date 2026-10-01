# React Roadmap (Laravel Developer Edition)

## Learning Flow
Concept -> Why -> Laravel Comparison -> When / When NOT -> Alternatives -> Internal Working -> Code -> Task -> Code Review -> Interview Q -> Revision

## Modules
| Level | Module | Difficulty | Interview Importance |
|---|---|---|---|
| 0 | JavaScript Foundation | Easy-Medium | 🔥 VERY HIGH |
| 1 | React Basics | Easy | 🔥 VERY HIGH |
| 2 | Hooks | Medium-Hard | 🔥 VERY HIGH |
| 3 | Architecture | Medium | 🟠 HIGH |
| 4 | Routing | Easy-Medium | 🟠 HIGH |
| 5 | API Integration (Laravel) | Medium | 🔥 VERY HIGH |
| 6 | Authentication | Hard | 🔥 VERY HIGH |
| 7 | Forms | Medium | 🟠 HIGH |
| 8 | State Management | Hard | 🔥 VERY HIGH |
| 9 | Performance | Hard | 🟠 HIGH |
| 10 | Advanced React | Hard | 🟡 MEDIUM-HIGH |
| 11 | React Internals | Hard | 🟠 HIGH (senior rounds me 🔥) |
| 12 | Testing | Medium | 🟡 MEDIUM |
| 13 | TypeScript | Medium | 🟠 HIGH |
| 14 | Production | Medium | 🟡 MEDIUM |
| 15 | HRMS Project | Hard | 🔥 Portfolio proof |

## Dependency Map
```text
JS -> React Basics -> Hooks -> Architecture -> Routing -> API -> Auth -> Forms
                        |                                              |
                        v                                              v
                   Internals                          State Mgmt -> Performance -> Advanced
                                                              |
                                          TypeScript -> Testing -> Production -> HRMS Project
```

## Laravel -> React Mental Model
> Ye sirf mental model samajhne ke liye comparison hai. Internally dono differently work karte hain.

| Laravel | React | Jahan comparison toot-ta hai |
|---|---|---|
| Route | React Router | Laravel server pe resolve hota hai, React browser me |
| Blade Component | React Component | Blade server pe HTML banata hai, React browser me UI update karta hai |
| Blade Props | React Props | React props read-only hote hain |
| Controller/API | API service layer | Business logic ka source backend hi rehta hai |
| Validation | Frontend + Backend | Frontend validation sirf UX, security backend se |
| Middleware | Protected routes + API auth | React guard sirf UI hide karta hai, security nahi |
| Session/Auth | Auth state | State refresh pe jaati hai, isliye /me API chahiye |
| DB state | Server state | Server state cache/stale hoti hai |

## Final Project Architecture
```text
React (Vite) -> pages/components/hooks -> services (axios) -> auth context/router guards
      | HTTPS JSON (Sanctum cookie/token)
Laravel: Route -> Middleware -> FormRequest -> Controller -> Service -> Model -> MySQL
```
