# GradFlow — Graduation Project Management System

A bilingual (Arabic/English), responsive graduation-project management web app prototype.

## Included
- RTL Arabic and LTR English interface with instant language toggle
- Dashboard with project metrics, progress visualization, activity feed, and deadlines
- Project list with search and status filters
- Add project and add task dialogs
- Task completion tracking
- Teams and members view
- Timeline, submissions placeholder, supervisor reviews, reports
- CSV report export
- Demo sign-in and local browser persistence

## Run locally
No build tools are required for this demo:
1. Extract the ZIP.
2. Open `index.html` in a modern browser.
3. Click **Demo sign in**. Use any email, password, and role; this is only a demonstration login.

For a local development server, run:
```bash
python -m http.server 8000
```
Then visit `http://localhost:8000`.

## Deploy the front-end demo
- Netlify: drag the extracted folder into Netlify Drop.
- Vercel: import the folder through a Git repository or deploy it as a static site.
- GitHub Pages: upload the files to a repository and enable Pages.

## Important production security note
This package is a working front-end demo, not a production-secure multi-user service yet. Demo sign-in does **not** authenticate a real user; data is stored in that browser's `localStorage`, and each browser has its own copy. Do not use it for real student records or confidential documents until you connect a backend.

## Recommended production backend: Supabase
Create a Supabase project, enable email/password authentication, and implement tables with Row Level Security (RLS):
- `profiles` (id references `auth.users`, full_name, role, department)
- `teams` (id, name, leader_id, supervisor_id)
- `team_members` (team_id, user_id)
- `projects` (id, team_id, title_ar, title_en, description, status, progress, deadline)
- `tasks` (id, project_id, title_ar, title_en, assignee_id, priority, status, due_date)
- `submissions` (id, project_id, uploaded_by, storage_path, version, review_status, feedback)
- `milestones` (id, project_id, title, due_date, status)
- `evaluations` (id, project_id, evaluator_id, score, comments)

Production requirements:
1. Restrict `admin` role assignment to a trusted server-side process; never trust a role supplied by the browser.
2. Enable RLS on every table and write policies for admin, supervisor, and team-member access.
3. Keep service-role keys on the server only. Never place them in front-end JavaScript.
4. Use private Storage buckets and signed URLs for submissions.
5. Configure password reset, email verification, backups, and audit logs.
6. Add tests for authorization, validation, and upload permissions before real deployment.

## Project structure
- `index.html` — application shell
- `styles.css` — responsive dark UI
- `app.js` — bilingual UI and demo interactions
