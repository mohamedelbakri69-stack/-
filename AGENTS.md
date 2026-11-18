# AGENTS.md — مِداد (Arabic teacher dashboard)

An Arabic, right-to-left dashboard for a Moroccan high-school Arabic teacher. **Read `PLAN.md` first.** Milestone 1 (the UI on sample data) is done. Continue with the next unchecked milestone.

## Architecture
- **TanStack Start + React 19** with file routes in `src/routes/`. `src/routeTree.gen.ts` is generated, so don't edit it.
- `src/routes/__root.tsx`: `<html lang="ar" dir="rtl">`, Google Fonts, `StoreProvider`, `AppShell`.
- Routes: `index.tsx` (dashboard), `students.index.tsx` (list, search params `classId`, `filter=struggling`, `q`, `sort`), `students.$studentId.tsx` (profile), `tasks.tsx`, `curriculum.tsx`.

## Key directories
- `src/lib/types.ts`: domain types (ClassGroup, Student, Assessment, Homework, Lesson, Task).
- `src/lib/fixtures.ts`: **the only source of sample data.** It uses a seeded PRNG and a fixed `REFERENCE_DATE` (2026-11-10) so SSR and hydration match. Swap this module for DB queries in milestone 2.
- `src/lib/analytics.ts`: pure derived logic: student summaries, struggling rules (`RISK_RULES`, `isStruggling`), class stats, grade bands, weekly attendance, lesson-plan progress, task due states, the timeline and the CSV export.
- `src/lib/store.tsx`: React context for the session-level task and lesson state (toggle, add, remove, weekly recurrence).
- `src/components/`: `AppShell` (sidebar nav with badges), `ui.tsx` (StatTile, Pill, Progress, PageHeader, ScoreBadge, Avatar), `charts.tsx` (Chart.js, client-only mount).

## Conventions
- All UI text is Arabic, and layout uses logical Tailwind utilities (`ms-`, `ps-`, `start-`). Chart x-axes use `reverse: true` and the y-axis sits on the right.
- Wrap numbers in `.num` (LTR isolate, tabular). Scores use comma decimals (`12,50`) via `formatScore`. Dates use Moroccan month names (شتنبر، نونبر، دجنبر…) via `formatDate`.
- Theme tokens live in `src/styles.css` `@theme` (paper, ink, teal, clay, saffron, good, bad). Each class has a `color` used consistently across screens.
- Tasks deliberately have **no priority field**. Only the due date and overdue state matter (the user asked for this).
- Browser-only work (Chart.js, downloads, `window.print`) goes in effects or event handlers.

## Non-obvious decisions
- "Struggling" = average < 10 **or** at least two risk reasons fire. Thresholds are shown to the teacher on the students page.
- Attendance stores only absences and late arrivals. Sessions are derived from each class's weekdays, minus the autumn break.
- Completing a recurring task appends its next weekly occurrence.
- When persistence arrives, use Netlify Database (Drizzle, `db/schema.ts`), not in-memory or JSON files.
