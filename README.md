# مِداد — Arabic Teacher Dashboard

**مِداد** is a right-to-left Arabic dashboard for a high-school (الثانوي التأهيلي) Arabic-language teacher. It follows five classes of 33–38 students each. In one place it shows statistics, student follow-up (grades, attendance, behavior, participation, tests and homework), alerts for struggling students, the yearly lesson plan (التوزيع السنوي) and tasks with overdue alerts.

## Screens

| Route | Screen |
| --- | --- |
| `/` | **لوحة القيادة**: alert strip (overdue tasks, struggling students, classes behind the lesson plan), six headline stats, class averages, grade distribution, weekly attendance trend, class cards, this week's tasks and the struggling-students list |
| `/students` | **التلاميذ**: filter by class, search by name or Massar code, "struggling only" toggle, sorting, and CSV export of the list |
| `/students/:id` | **الملف الشخصي**: alert banner, stat tiles, tabs (follow-up timeline, grades with class average and rank, attendance, homework, behavior and participation), grade chart, council summary, **CSV download** and **print / PDF** |
| `/tasks` | **المهام**: no priorities. Tasks are grouped by due date (overdue, today, the next 7 days, later, done). Weekly recurring tasks such as lesson prep reschedule themselves when completed |
| `/curriculum` | **التوزيع السنوي**: planned vs. completed lessons per class, behind/ahead indicators, and lessons you can tick off as done |

## Tech

- TanStack Start (React 19, file-based routes) on Netlify
- Tailwind CSS v4 with a custom paper/ink theme and fonts (Reem Kufi, IBM Plex Sans Arabic, Amiri)
- Chart.js via `react-chartjs-2` (RTL axes and tooltips)
- `lucide-react` icons

All data is currently realistic **sample data** from `src/lib/fixtures.ts`, generated with a seeded random generator so it stays stable. Task and lesson changes last for the browser session.

## Run locally

```bash
pnpm install
netlify dev        # or: pnpm dev
```

## Roadmap

See [PLAN.md](./PLAN.md). Next steps: permanent storage in Netlify Database, real class lists (Massar import), daily attendance and grade entry, a behavior and participation log, the teacher's own login, PDF profiles, and alerts by email.
