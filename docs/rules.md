# Project Rules — SchoolOS

These rules apply to all contributors and AI coding agents. Prioritize a **working, secure MVP** over speculative architecture or visual polish.

## Product and scope
1. Build only requirements in `PRD.md` P0 unless an explicit decision is recorded in `memory.md`.
2. Implement end-to-end vertical slices: database → API → authorization → UI → tests.
3. No microservices, Kubernetes, Kafka, Temporal, AI or native app in MVP.
4. Never hardcode school branding or fork frontend code per school.
5. Every new feature requires a user story and acceptance criteria.
6. Prefer simple, maintainable solutions; document deliberate trade-offs.

## Coding conventions
7. TypeScript strict mode in frontend/backend; no unexplained `any`.
8. Use meaningful names, small functions and module boundaries; avoid premature abstraction.
9. Validate all external inputs with shared Zod schemas; handle errors centrally.
10. Keep API routes thin; business logic in services; DB access in repositories or clearly bounded services.
11. Use Prisma migrations; never manually modify production schema.
12. Avoid N+1 queries; paginate large collections and index frequent tenant queries.
13. No credentials in code, docs, screenshots or commits; keep `.env.example` safe.
14. Use consistent REST endpoints and error shapes; document API changes.

## Security and privacy (non-negotiable)
15. Derive `schoolId` from trusted tenant context and authorized membership, not request payload.
16. Every tenant-scoped read/write must check school and resource ownership.
17. Teachers may access only assigned sections/subjects; guardians only verified linked children.
18. Never reveal unpublished results, other students' details or fee records.
19. Use secure sessions/cookies, password hashing, CSRF defenses, login rate limits and server-side permission checks.
20. Log sensitive modifications with actor, timestamp and entity; never log secrets or full child records.
21. File uploads must validate MIME/type, size, permissions and storage access.
22. Financial data uses integer paise or fixed decimal and transactions; never JS floating point for money.
23. Do not silently delete academic or financial history; use defined retention and archival workflows.
24. Legal/privacy review is required before using real minors' data; no real personal data in dev or demo fixtures.

## UX and accessibility
25. Mobile-first responsive layout; every critical flow usable on a basic phone.
26. Keep forms concise, label fields clearly and show validation near inputs.
27. Always include loading, empty, error and success states.
28. Do not use color alone to communicate attendance, fee status or grades.
29. Use reusable design tokens; school colors cannot compromise contrast or readability.
30. Confirm destructive actions; preserve user-entered data on recoverable errors.

## Testing and release
31. Add unit tests for grades, balances and permission logic.
32. Add integration tests for all tenant-scoped APIs, including cross-tenant negative cases.
33. Add E2E tests for onboarding, attendance, result publishing and fee recording.
34. No merge if lint/typecheck/tests fail; peer review changes affecting auth, marks or fees.
35. No production pilot without backup restore test, audit logs, monitoring and migration rollback plan.
36. Each task is done only when acceptance criteria pass and docs are updated.

## Workflow for contributors/AI agents
37. Read `memory.md`, `PRD.md`, `architecture.md`, and `task.md` before implementing a task.
38. Work on the next unchecked task; do not implement unrelated features.
39. State assumptions, changed files, migrations, test results and known limitations in handoff notes.
40. Record architectural decisions and unresolved questions in `memory.md`.
41. If requirements conflict, ask for a decision instead of silently broadening scope.
42. Never claim tests passed unless they actually ran.
