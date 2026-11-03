# Project Memory — SchoolOS

**Purpose:** Persistent, editable project context for future contributors and AI assistants. This file records decisions, progress, assumptions and unresolved questions. Update after each meaningful development session. It is not a place for credentials or student data.

## 1. Project summary
- **Working name:** SchoolOS (placeholder; not final brand).
- **Idea:** Subscription-based multi-tenant, white-label SaaS for Indian schools.
- **Buyer:** School; **users:** platform admin, school admin, teacher, student, guardian.
- **Core value:** One branded portal for records, attendance, results, fees and basic school operations.
- **Priority:** Build a working MVP before optimizing architecture or visual polish.
- **Status:** Planning/documentation; no implementation is assumed complete.
- **Date initialized:** 2026-10-28.

## 2. Decisions made
| ID | Decision | Reason | Status |
|---|---|---|---|
| D-001 | Responsive web first | Fastest path to pilot | Proposed baseline |
| D-002 | Modular monolith | Lower complexity | Proposed baseline |
| D-003 | PostgreSQL + Prisma | Relational data, transactions | Proposed baseline |
| D-004 | Next.js + Node/Express + TypeScript | Familiar full-stack development | Proposed baseline |
| D-005 | Shared database with tenant IDs | Simple early multi-tenancy | Proposed baseline |
| D-006 | Config-driven branding | One codebase for every school | Confirmed product direction |
| D-007 | Offline fee recording first | Avoid early payment gateway complexity | Proposed baseline |
| D-008 | Redis optional, not required at start | Build only needed infrastructure | Proposed baseline |
| D-009 | School verifies student/guardian account links | Prevent unauthorized child data access | Required security rule |

## 3. MVP scope
- School onboarding, profile and branding.
- Roles and school-scoped authentication.
- Academic sessions, classes, sections, subjects.
- Student/teacher records and verified guardian links.
- Attendance, exams/results, fee charges/offline payments.
- Student and guardian read-only views of authorized records.
- CSV import, basic notices, export, audit and subscription states.

## 4. Explicit non-goals for MVP
Online payments, AI, payroll, transport/GPS, library, live chat, native apps, microservices, Kubernetes, Kafka, complex analytics, automatic government integrations, and advanced custom domains.

## 5. Current progress
- [x] Initial product concept and stakeholder requirements discussed.
- [x] MVP-oriented project documentation drafted.
- [ ] Confirm first pilot school and detailed workflows.
- [ ] Scaffold repository and local development environment.
- [ ] Implement first vertical slice.
- [ ] Conduct security/privacy readiness review.
- [ ] Launch pilot.

## 6. Open questions
1. Final product name and domain?
2. Which board(s), classes and school size for first pilot?
3. Who verifies student and guardian invitations?
4. What grading policies and report card layout does pilot school require?
5. Which fee heads, concessions, payment methods and receipt numbering apply?
6. How long are subscription grace and read-only periods?
7. What is the retention/export/deletion policy and school contract model?
8. Which cloud provider/region and transactional email provider?
9. Should notices be in first demo or only pilot?

## 7. Development session log
### 2026-10-28 — Documentation baseline
- Created six project docs: `PRD.md`, `architecture.md`, `rules.md`, `design.md`, `task.md`, `memory.md`.
- Defined first vertical slice: school login → class/student setup → teacher attendance → student view.
- No code, database, deployment or tests have been completed by this documentation task.

### Template for next entry
```md
### YYYY-MM-DD — Short description
- Completed:
- Files/modules changed:
- Migrations:
- Tests executed and results:
- Decisions made:
- Blockers/next task:
```

## 8. AI/developer handoff checklist
Before work: read `memory.md`, then `PRD.md`, `architecture.md`, `rules.md`, `task.md` and `design.md` as needed. Choose the next unchecked task. After work: report actual changes/tests and update this file; do not mark incomplete work done.

## 9. Change control
- Record changes to MVP scope in `PRD.md` and this file.
- Record architecture changes as new ADRs in `architecture.md`.
- Keep `task.md` aligned with implemented features, not aspirational claims.
- Never put secrets, real student records, access tokens or passwords here.
