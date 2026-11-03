# UI/UX Design Specification — SchoolOS MVP

**Design goal:** A clean, trustworthy, fast school portal that works on phones and desktop. Build reusable screens first; improve visual refinement after core workflows function.

## 1. Design principles
- Clarity before decoration: simple navigation, obvious actions and legible tables.
- School-branded, not school-forked: one shared design system with configurable logo, name and accent.
- Accessibility: keyboard navigation, labels, visible focus, adequate contrast and semantic status labels.
- Mobile first: teachers should mark attendance on a phone without horizontal scrolling.
- Progressive complexity: only show actions allowed for the current role.

## 2. School branding configuration
```ts
type SchoolTheme = {
  schoolName: string;
  logoUrl?: string;
  primaryColor?: string; // validated hex
  address?: string;
  contactEmail?: string;
};
```
Use neutral surfaces, readable text and a small set of semantic colors. Validate school accent contrast; fall back to a safe primary color. Never accept arbitrary CSS/HTML from tenants. School slug determines branding; permission checks determine data.

## 3. Suggested design tokens (starting defaults)
```css
:root {
  --brand: #2563eb;
  --background: #f8fafc;
  --surface: #ffffff;
  --text: #0f172a;
  --muted: #64748b;
  --border: #e2e8f0;
  --success: #15803d;
  --warning: #b45309;
  --danger: #b91c1c;
  --radius: 12px;
  --space: 8px;
}
```
Use a consistent 8px spacing scale, 16px minimum body text on small screens where feasible, and accessible hit targets. Avoid large animation libraries for MVP.

## 4. Information architecture
### Public / auth
- Platform landing (simple), school login, invitation acceptance, password reset.
### School admin
- Overview; Students; Staff; Academics; Attendance; Exams & Results; Fees; Notices; School Settings.
### Teacher
- My Classes; Attendance; Marks; Notices; Profile.
### Student
- Overview; Attendance; Results; Fees (view only); Notices; Profile.
### Guardian
- Child switcher; Child Overview; Attendance; Results; Fee Status; Notices.
### Platform admin
- Schools; Subscription Status; Support/Audit (limited); Platform Settings.

## 5. Screen inventory and MVP layout
1. **School login:** school logo/name, email/password, recovery link, clear errors.
2. **Admin overview:** enrollment, attendance snapshot, unpaid balance summary, quick actions.
3. **Student directory:** searchable table on desktop, stacked cards on mobile, add/import controls.
4. **Student detail:** identity, current enrollment, attendance, published results, fee summary.
5. **Teacher class view:** assigned classes/subjects and attendance action.
6. **Attendance sheet:** date, class, roster, present/absent/late toggle, save status, unsaved warning.
7. **Exam setup and marks:** exam list, subject max marks, editable draft marks, publish confirmation.
8. **Result view:** only published results; print-friendly school-branded report.
9. **Fee ledger:** charges, payments, allocations, outstanding amount, receipt actions.
10. **Branding settings:** upload logo, edit school address/name/color, live preview.
11. **Invitation/guardian linking:** approved account activation and child access verification.
12. **Notices:** list of school announcements and simple admin editor.

## 6. Core wireframes (text)
### Desktop admin
```text
+-----------------------------------------------------------+
| [School logo] School Name        Search       User menu   |
+------------+----------------------------------------------+
| Overview   |  Dashboard                                  |
| Students   |  [Students] [Today's Attendance] [Dues]      |
| Staff      |                                              |
| Academics  |  Quick Actions: Add Student | Mark Attendance|
| Attendance |  Recent Notices / Upcoming Exams             |
| Exams      |                                              |
| Fees       |                                              |
+------------+----------------------------------------------+
```
### Mobile attendance
```text
[Back] Class 8-A               [Date]
Present 29 / Total 32
[Search student]
Student 01   [Present] [Absent] [Late]
Student 02   [Present] [Absent] [Late]
...
[Save Attendance]
```

## 7. UI component library
Button, Input, Select, DatePicker, Dialog, Toast, Tabs, Badge, Avatar, DataTable, MobileList, EmptyState, ErrorState, Skeleton, FileUpload, Pagination, ConfirmDialog, RoleGuard, SchoolHeader, FeeAmount, AttendanceStatus. Build components only as screens need them.

## 8. States and edge cases
- Loading: skeleton/inline progress for slow networks.
- Empty: explain how to add first student/class/exam.
- Errors: show actionable retry; preserve unsaved forms.
- Unauthorized: clear message and safe navigation; never display cached foreign-tenant data.
- Subscription grace/read-only: visible banner with contact/admin guidance.
- Fee amounts: Indian currency formatting (₹), explicit due dates and receipt status.
- Published results: distinguish draft, reviewed and published states.
- Import: preview rows and errors before committing.

## 9. Design implementation order
1. Layout shell + school branding + login.
2. Reusable forms, tables/cards, empty/error states.
3. Students/classes + teacher attendance.
4. Results and fees workflows.
5. Responsive polish, accessibility audit, print styles.
6. Later: animations, advanced charts, custom themes, native app.

## 10. Design acceptance checklist
- [ ] Works at 360px mobile width and desktop.
- [ ] No horizontal overflow on core forms.
- [ ] School logo and accent update without redeploy.
- [ ] All actions are keyboard reachable with focus indicator.
- [ ] Status conveyed by text/icon as well as color.
- [ ] Every role sees appropriate navigation only.
- [ ] Result/receipt print layouts are readable.
- [ ] Loading, empty, error and success states implemented.
