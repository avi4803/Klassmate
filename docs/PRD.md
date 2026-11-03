# Product Requirements Document — SchoolOS

**Status:** Draft v0.1 | **Product:** Multi-tenant school management SaaS for Indian schools | **Primary goal:** Ship a usable MVP to one pilot school.

## 1. Problem and vision
Indian schools often coordinate student records, attendance, results, fee dues, and announcements across registers, spreadsheets, and messaging tools. SchoolOS provides one school-branded portal for administrators, teachers, students, and guardians. The platform operator sells subscriptions to schools; students do not buy individual subscriptions.

**MVP promise:** A school can onboard, create classes, add students and teachers, record attendance, publish exam results, track fee dues/payments, and allow verified students/guardians to view their own records.

## 2. Target customer and assumptions
- **Initial customer hypothesis:** Indian private schools with ~200–1,500 students; validate through interviews.
- **Buyer:** Principal, owner, trust, or authorized school administrator.
- **Users:** Platform admin, school admin, teacher, student, guardian.
- **Delivery:** Responsive web app first; native mobile later.
- **Board support:** Board-neutral MVP with configurable class names, sessions, subjects, exams and grading; no claim of official CBSE/CISCE/UDISE+ integration.

## 3. MVP boundaries
### In scope (P0)
1. Platform admin creates/approves school and manages subscription state manually.
2. School profile: name, address, logo, primary color, slug; shared templates, no custom code per school.
3. Authentication and role-based access; school-admin invites teachers, students and guardians; verified student/guardian linking.
4. Academic sessions, classes, sections, subjects and teacher assignments.
5. Student records and annual enrollments; CSV import with preview, validation and error report.
6. Daily attendance by assigned teacher; school admin corrections audited.
7. Exams, marks entry, draft/publish results and student report view; simple configurable numeric/grade rules.
8. Fee structures, charges, offline payment recording, outstanding balances and receipts; payment gateway **not** in MVP.
9. Role-specific dashboards; school notices as a simple read-only feed.
10. School subscription states: trial, active, grace, read-only, suspended; data export for authorized school admin.

### Explicitly out of scope for MVP
Online fee collection, payroll, transport/GPS, library, homework/LMS, live chat, AI recommendations, native apps, custom domains, advanced analytics, automatic government-system integration, multi-campus hierarchies, complex timetable optimization, and automated SaaS billing.

## 4. Core user journeys
1. **Onboard school:** Platform admin approves a school → school admin enters profile/branding → configures academic session and classes.
2. **Import students:** School admin uploads CSV → reviews validation results → confirms import → records are created with school-scoped unique admission numbers.
3. **Take attendance:** Assigned teacher opens class/date → marks present/absent/late → submits → admin can audit changes.
4. **Publish results:** Admin configures exam/subjects → teacher enters marks → admin reviews and publishes → linked student/guardian can view.
5. **Track fees:** Admin creates fee charges → records cash/bank/cheque payments → balance recalculates → guardian views dues and receipt.
6. **Activate account:** Admin invites user → user verifies invitation → server links only approved enrollment/guardian relationship.

## 5. Roles and permissions (summary)
| Action | Platform admin | School admin | Teacher | Student | Guardian |
|---|---|---|---|---|---|
| Manage schools/subscriptions | Yes | No | No | No | No |
| Manage own school branding | No* | Yes | No | No | No |
| Manage students/classes | No* | Yes | Assigned view | Own view | Linked child view |
| Submit attendance | No | Correct/audit | Assigned class | View own | View linked child |
| Enter exam marks | No | Review/correct | Assigned subject | Published only | Published linked child |
| Manage fee ledger | No | Yes | No | View own | View linked child |
| Export school data | No* | Yes | No | Own data as permitted | Linked child as permitted |

*Platform support must use explicit, audited, time-limited access; never default unrestricted access to tenant records.

## 6. Functional requirements and acceptance criteria
- **FR-01 Tenant creation:** Each school has unique ID and slug; branding is loaded by resolved tenant; no data leaks across schools.
- **FR-02 Auth:** Login/logout, invite acceptance, password reset, role checks; unauthorized operations return 403 and unauthenticated operations 401.
- **FR-03 Academics:** School admin creates a session, class, section, subject and assignments; cannot create duplicate class/section for same session.
- **FR-04 Student management:** Admission number unique per school; student retains permanent identity across enrollments and years.
- **FR-05 Attendance:** One record per enrollment/date; only assigned teacher/admin can write; edits include actor/time/reason.
- **FR-06 Exams:** Marks validated within allowed range; draft results inaccessible to students; publish action audited.
- **FR-07 Fees:** Charges, payments and adjustments form an auditable ledger; partial payments supported; duplicate receipt/reference blocked.
- **FR-08 Dashboards:** Every role sees only authorized school and student information.
- **FR-09 Branding:** Logo/color/name/address appear on login, navigation and printable reports, with safe defaults.
- **FR-10 Import:** Invalid rows produce downloadable errors; successful imports are idempotent or duplicates are flagged.
- **FR-11 Subscription:** Expiry follows configured grace/read-only policy; no silent deletion of school data.
- **FR-12 Export:** School admin can export its student, attendance, results and fee records in documented formats.

## 7. Non-functional requirements (initial engineering targets)
- Responsive UI on low-end phones and desktop; keyboard-accessible forms; WCAG 2.2 AA as a target.
- p95 read API latency < 500 ms in pilot load tests; measured, not promised SLA.
- No cross-tenant reads/writes in automated integration tests; all tenant-scoped routes tested.
- HTTPS in production, strong password hashing, rate limits, audit trail, safe uploads and backups.
- Daily automated database backups with documented restore drill before production pilot.
- Structured logs and error monitoring; do not log passwords, tokens, child records or financial secrets.
- Hindi-ready internationalization architecture; English interface in first release.

## 8. Success metrics
- First school onboarded without code changes or manual database edits.
- School admin imports 100 students with a clear validation report.
- Teacher records attendance for one class in under 3 minutes in a usability test.
- Admin publishes a test exam and a verified student sees only their result.
- Partial fee payment yields correct outstanding balance and receipt.
- Cross-tenant access tests pass; restore drill succeeds; pilot stakeholders sign off.

## 9. Risks, research and compliance
- Interview 5–10 schools to validate purchasing, workflows, fee practices and report card requirements.
- Child-data privacy and India's applicable DPDP requirements need qualified legal review; document consent, notices, retention and guardian verification before pilot.
- Check applicable GST/invoicing treatment for SaaS and school payments with a professional.
- Do not promise official board/UDISE+ integration without verified authorization.
- Payment gateway and messaging providers introduce fees, reconciliation, consent and operational obligations; defer.

## 10. Release gates
**Demo gate:** Single school can complete all core journeys using seeded test data.
**Pilot gate:** Multi-tenant authorization, backups, audit logs, error handling, onboarding, privacy notices and pilot UAT completed.
**Scale gate:** Only after real adoption and measured bottlenecks; see `architecture.md`.

## 11. Open decisions
Product name; first pilot school and board; who approves student/guardian invitations; fee head/receipt rules; exam grading rules; grace-period duration; data retention schedule; hosting region/provider; branding defaults.
