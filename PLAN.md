# PLAN — مِداد roadmap

A dashboard for one Arabic teacher in a Moroccan high school (5 classes, about 176 students). Every milestone is a small piece of work that can ship on its own.

## ✅ Milestone 1: product surface (done)
- Arabic RTL app shell and visual identity
- Home dashboard: alerts, headline stats, charts, class cards, tasks, struggling students
- Students list (filters, search, sort, CSV export) and student profile (timeline, tabs, CSV and print/PDF)
- Tasks page (no priorities, overdue alerts, weekly recurrence, add/complete/delete)
- Yearly lesson plan page (planned vs. done, toggle lessons)
- All data comes from `src/lib/fixtures.ts`. Interactive changes live in `src/lib/store.tsx` and last only for the session

## Milestone 2: data model and persistence (Netlify Database + Drizzle)
- `db/schema.ts`: classes, students, assessments, grades, sessions, attendance, homework, homework_status, behavior_notes, participation, lessons, tasks
- Seed script that loads the current fixtures so the UI looks identical afterwards
- Replace module-level fixture reads in `src/lib/analytics.ts` with server functions and route loaders
- Replace the `store.tsx` setters with server functions for tasks and lessons

## Milestone 3: teacher login
- Netlify Identity sign-in (single teacher account). Every route and server function is gated

## Milestone 4: class and student management
- Create/edit classes, then import class lists from a Massar export (CSV/XLSX)
- Edit student details (guardian contact, notes)

## Milestone 5: daily entry screens
- One-tap attendance per session (present / absent / late, justified flag)
- Grade entry grid per assessment (scores out of 20, comma decimals) and creation of tests and activities
- Homework assignment and status checklist
- Quick behavior/participation notes from the class roster

## Milestone 6: lesson plan editor
- Import or edit the yearly plan per level (units, lessons, components, planned weeks)
- Holiday calendar so "expected progress" ignores breaks
- Link "lesson prep" recurring tasks to the next planned lesson automatically

## Milestone 7: alerts and reports
- Configurable struggling-student thresholds (currently `RISK_RULES` in `analytics.ts`)
- Scheduled function for a daily digest of overdue tasks and new struggling students (email)
- Server-generated PDF profile and class report for the class council (مجلس القسم)
- Semester switch (الدورة الأولى / الثانية) and year archive

## Milestone 8: polish
- Mobile-first quick-entry mode, offline-friendly attendance, dark theme
