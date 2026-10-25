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
- Firebase email/password sign-in with verified-email requirement
- Per-user Cloud Firestore persistence, protected by the included security rules

## Run locally
No build tools are required:
1. Serve the files from a local web server (Firebase modules need HTTP/HTTPS; opening the file directly will not work).
2. Create an account with an email address, verify the link Firebase sends, then sign in.

For a local development server, run:
```bash
python -m http.server 8000
```
Then visit `http://localhost:8000`.

## Firebase setup
This repository is connected to the NEXORA Firebase web app. The browser configuration in `firebase.js` contains public Firebase client metadata, not an access credential. Firestore rules are the security boundary and keep each verified account's workspace data under that account's own user ID.

Before using the live app:
1. Keep **Email/Password** sign-in enabled in Firebase Authentication.
2. Add the deployed GitHub Pages domain to Authentication's authorized domains if Firebase requests it.
3. Publish `firestore.rules` in Firebase Console → Firestore Database → Rules.
4. Keep the catch-all deny rule. Never put service-account credentials in this static site.

The current interface does not provide team-wide role-based access. Each account sees its own workspace; sample projects are starter data.

## Deploy the front end
- Netlify: deploy the folder as a static site.
- Vercel: import the Git repository or deploy as a static site.
- GitHub Pages: serve the repository from its Pages deployment.
