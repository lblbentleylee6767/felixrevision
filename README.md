# Felix Revision Hub — V1.0

A responsive Year 8 Geography revision website for Felix. Built with React + Vite and designed for deployment as a Render Static Site.

## Included
- Student dashboard and navigation
- Development topic notes based on the supplied `Y8 revision and guidance.pptx`
- 12 flashcards with self-rating
- 20-question multiple-choice practice test with marking and explanations
- Mind map overview
- Mistake book and revision history
- Progress summary
- Admin sign-in and revision-session publishing interface
- Supabase schema and Render blueprint

## Important behaviour / limitations
- Without Supabase credentials, the website still works as a static revision site. Student activity is stored in that browser's local storage only.
- To enable administrator login and publish sessions to a shared database, configure Supabase as below.
- Student progress is currently device/browser-local, not synced between devices or users.
- The included starter learning content is focused on the Development topic from the uploaded revision organiser. Some quiz questions are practice questions derived from those definitions, not official exam questions.
- The exam date shown is Tuesday, 24 November 2026, as supplied by the site owner.

## Run locally
1. Install Node.js 20 or newer.
2. Extract this ZIP.
3. In the project folder run:
   ```bash
   npm install
   npm run dev
   ```
4. Open the local URL printed by Vite.

## Deploy to Render
1. Push this project folder to a GitHub repository.
2. In Render choose **New + → Blueprint** and connect the repository (or create a Static Site).
3. `render.yaml` defines the build command `npm install && npm run build` and publish directory `dist`.
4. Deploy. Render gives you a temporary `onrender.com` address.
5. Test the website before adding your custom domain.

## Optional: Supabase shared content publishing
1. Create a Supabase project.
2. Open SQL Editor and run `supabase/schema.sql`.
3. In Authentication, create Bentley's administrator user.
4. Promote that user to admin by setting the user's **app_metadata** to:
   ```json
   {"role":"admin"}
   ```
   Do this only from a trusted server-side/admin environment or Supabase dashboard tooling. Never put a service-role key in this website.
5. In Render Environment, set:
   - `VITE_SUPABASE_URL` = Project URL
   - `VITE_SUPABASE_ANON_KEY` = publishable/anon key
6. Redeploy the site.
7. Sign in through Admin Panel. New revision sessions will be written to Supabase and shared to visitors.

The browser bundle uses only the Supabase publishable/anon key. Database RLS is the security boundary. Never expose a Supabase service-role key in frontend code.

## Custom domain felixrevision.com
1. Register `felixrevision.com` with a domain registrar first; it is not included with this project.
2. In Render open the Static Site → Settings → Custom Domains and add `felixrevision.com` (and optionally `www.felixrevision.com`).
3. Follow the exact DNS records Render displays at your registrar. DNS values can vary; do not copy guessed records.
4. Wait for DNS verification and TLS certificate provisioning. Set the preferred domain/redirect in Render.

## Content source
The initial Geography notes preserve key definitions and causes/solutions from the user's uploaded Year 8 Revision and Guidance presentation. Where the presentation asks questions without supplying answers (for example, explaining each cause of poverty or each way to close the development gap), this starter site does not invent full source answers.

## Updating content
- For static content: edit `src/data.js` and redeploy.
- With Supabase enabled: sign in as admin and publish a new revision session from Admin Panel.
