# Implementation Task Board — SchoolOS

**Operating rule:** Complete one thin vertical slice before broadening scope. `- [ ]` means not started; check items only after verifying acceptance criteria. Durations are estimates, not commitments.

## Milestone 0 — Project setup (1–3 days)
- [ ] Create monorepo `apps/web`, `apps/api`, `packages/shared`.
- [ ] Configure strict TypeScript, ESLint, formatter and environment validation.
- [ ] Add Docker Compose for PostgreSQL and `.env.example`.
- [ ] Configure Prisma migrations, seed and local start scripts.
- [ ] Set up unit/API/E2E test runners and CI typecheck/lint/test.
**Done when:** New developer can clone, run one command sequence and see web + API + DB healthy.

## Milestone 1 — First working vertical slice (1–2 weeks)
- [ ] Implement School, User, Membership, AcademicSession, Class, Section, Student, Enrollment tables.
- [ ] Seed two schools with distinct admins and sample students.
- [ ] Build login/logout with secure session cookies.
- [ ] Resolve school slug and enforce membership authorization.
- [ ] Build basic school-branded admin dashboard.
- [ ] Build class/section and student create/list screens.
- [ ] Add Teacher assignment and attendance write/read APIs.
- [ ] Build teacher attendance sheet and student attendance view.
- [ ] Add cross-tenant negative tests and teacher-assignment tests.
**Done when:** A teacher in School A marks attendance; School A student sees it; School B cannot access it.

## Milestone 2 — School onboarding and users (1–2 weeks)
- [ ] School creation/approval from platform admin (manual subscription state).
- [ ] Branding settings: logo/name/address/primary color.
- [ ] School admin invites teachers, students and guardians.
- [ ] Implement verified guardian-child linking.
- [ ] CSV import with validation preview and error report.
- [ ] Add role-specific navigation and profile views.
**Done when:** Second school onboards without code changes or direct database edits.

## Milestone 3 — Results (1–2 weeks)
- [ ] Implement Subject, Exam, ExamSubject and Mark entities.
- [ ] Configure max marks and basic grading policy.
- [ ] Teacher enters marks for assigned subjects.
- [ ] Admin reviews and publishes results; changes audited.
- [ ] Student/guardian sees published result only.
- [ ] Generate basic printable report card.
- [ ] Test out-of-range marks, unpublished visibility and cross-tenant access.
**Done when:** Full exam-to-report-card journey works with sample school data.

## Milestone 4 — Fees (1–2 weeks)
- [ ] Implement charges, payments, allocations and adjustments.
- [ ] Support partial offline payments and balance calculation.
- [ ] Generate unique numbered receipts; prevent duplicate posting.
- [ ] Build admin fee ledger and student/guardian fee view.
- [ ] Audit fee corrections and write financial transaction tests.
**Done when:** ₹5,000 charge + ₹2,000 payment yields ₹3,000 outstanding, with correct receipt and no double counting.

## Milestone 5 — Pilot readiness (2–4 weeks)
- [ ] Notices feed and school-wide publication.
- [ ] Subscription grace/read-only states and authorized export.
- [ ] Add password reset, login throttling, secure uploads, validation.
- [ ] Implement monitoring, structured logs and error alerts.
- [ ] Configure automated backups and execute restore drill.
- [ ] Review child-data privacy, notices, retention and school agreements with qualified counsel.
- [ ] Load-test critical screens; optimize slow queries.
- [ ] Test on mobile/low-bandwidth network; complete accessibility pass.
- [ ] Run school admin/teacher/student/guardian UAT and fix blocking issues.
**Done when:** Pilot school signs off; data recovery and security gates pass.

## Milestone 6 — After first pilot (do not start early)
- [ ] Interview users and rank pain points from actual usage.
- [ ] Add online payment gateway with webhook idempotency and reconciliation.
- [ ] Add Redis/BullMQ for slow jobs if measured need exists.
- [ ] Expand configurable grading, notifications and reports.
- [ ] Consider Hindi/localization, native apps and optional modules.

## Definition of done for every task
- [ ] Acceptance criteria met; role/tenant authorization checked.
- [ ] Unit/integration/E2E tests added as appropriate and executed.
- [ ] Loading/empty/error states handled on UI changes.
- [ ] No secrets or sensitive data logged.
- [ ] Relevant docs and `memory.md` updated.
- [ ] Migration/rollback impact documented if schema changed.

## Suggested first five tickets
1. `SETUP-001` Scaffold monorepo and Postgres Docker Compose.
2. `DATA-001` Prisma schema for School/User/Membership/AcademicSession/Class/Section/Student/Enrollment.
3. `AUTH-001` Session login + tenant resolution + RBAC middleware.
4. `STUDENT-001` School-scoped student create/list UI and API.
5. `ATTEND-001` Teacher class attendance and student attendance view.

## Dependencies and blockers
- Confirm school onboarding approval flow, academic session conventions, grading rules and fee receipt numbering before implementing those modules.
- Do not use real student data before privacy/legal readiness and pilot authorization.
