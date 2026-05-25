# Student Dashboard — Project Tasks

> **Total Tasks:** 230 across 17 phases  
> **Project:** Student Dashboard (React + Tailwind · FastAPI · Pydantic · MongoDB)  
> **Timeline:** Solo · ~6.5 months  
> **Stack:** React/Vite (frontend) · FastAPI/uvicorn (backend) · MongoDB Atlas + Motor (database) · Vercel + Render (deployment)

---

## How to Use This Document

Each section below is one phase of the build. Every task is a discrete, actionable unit. Complete phases sequentially unless noted otherwise. You can track progress by marking tasks complete with checkboxes as you go.

---

## Phase 0 — Planning & Design (15 tasks)

- [ ] 0.1 Re-read the README fully — confirm every widget's "Data Stored" section is final before writing any code.
- [ ] 0.2 Sketch the dashboard wireframe on paper: grid layout, header, widget-adding flow.
- [ ] 0.3 Sketch all four widgets (Note, Archive, Calendar, Form) in both compact and expanded states.
- [ ] 0.4 Sketch catalog/carousel view and table view (shared UI patterns across multiple widgets).
- [ ] 0.5 Define the color system: background, surface, border, text, accent, error — write hex values.
- [ ] 0.6 Decide how the first tag's color drives the widget header accent color — mock it on paper.
- [ ] 0.7 Pick typography: one display/heading font, one body font — configure both in Tailwind.
- [ ] 0.8 Map out all MongoDB collections: `users`, `boards`, `widgets`, `notes`, `archive_files`, `events`, `forms`.
- [ ] 0.9 Design each document schema — specify which fields are top-level vs nested.
- [ ] 0.10 Decide the ObjectId reference strategy (e.g. `note.linked_archive_ids: [ObjectId, ...]`).
- [ ] 0.11 List every API endpoint needed: method, path, purpose.
- [ ] 0.12 Decide file storage strategy for the Archive widget: local disk, GridFS, or Cloudinary.
- [ ] 0.13 Decide JWT storage strategy: httpOnly cookie vs localStorage — document the security tradeoff.
- [ ] 0.14 Choose deployment targets: Vercel (frontend), Render (FastAPI), MongoDB Atlas (database).
- [ ] 0.15 Set up a tracking board (GitHub Projects or Notion) for personal progress tracking.

---

## Phase 1 — Project Setup (17 tasks)

- [ ] 1.1 Create monorepo root folder with `/client` and `/server` subdirectories.
- [ ] 1.2 Initialize React + Vite in `/client`.
- [ ] 1.3 Install and configure Tailwind CSS v3 in `/client`.
- [ ] 1.4 Install `react-grid-layout`, `react-router-dom`, `axios` in `/client`.
- [ ] 1.5 Create `.env.example` in `/client` with a `VITE_API_URL` placeholder.
- [ ] 1.6 Add `.env` to `.gitignore` immediately — verify it's excluded before the first commit.
- [ ] 1.7 Create `/client/src` folder structure: `components/`, `pages/`, `hooks/`, `services/`, `store/`.
- [ ] 1.8 Set up a Python virtual environment in `/server`.
- [ ] 1.9 Install FastAPI dependencies: `fastapi`, `uvicorn[standard]`, `motor`, `pydantic[email]`, `python-jose[cryptography]`, `passlib[bcrypt]`, `python-multipart`.
- [ ] 1.10 Install `slowapi` (rate limiting) and `python-dotenv` in `/server`.
- [ ] 1.11 Create `/server` folder structure: `routers/`, `models/`, `schemas/`, `services/`, `middleware/`, `core/`.
- [ ] 1.12 Create `main.py` with a FastAPI app instance and a `GET /health` route returning 200.
- [ ] 1.13 Create `.env` for `/server` with keys: `MONGO_URI`, `SECRET_KEY`, `CORS_ORIGINS`, `ENV`.
- [ ] 1.14 Write `db.py` to initialize the Motor async client and expose collection handles.
- [ ] 1.15 Connect to MongoDB locally or Atlas — confirm a test insert and read both work.
- [ ] 1.16 Confirm `/client` dev server and `/server` uvicorn run simultaneously without conflict.
- [ ] 1.17 Make the first commit with a working skeleton: health check passes, DB connects.

---

## Phase 2 — Security Planning (8 tasks)

- [ ] 2.1 Document the exact CORS origins to allow — no wildcard `*`, list them explicitly.
- [ ] 2.2 Plan JWT configuration: algorithm (`HS256`), expiry time (e.g. 7 days), payload claims (`sub=user_id`).
- [ ] 2.3 Plan httpOnly cookie config: `httponly=True`, `secure=True`, `samesite='lax'`.
- [ ] 2.4 Plan rate limiting targets: `/auth/login` (5/minute), `/upload` (10/minute).
- [ ] 2.5 Plan file upload security: MIME type allowlist, max file size limit, UUID-based server-side filenames.
- [ ] 2.6 Plan markdown/HTML sanitization — decide which HTML tags are safe to render (bleach allowlist).
- [ ] 2.7 Plan error response policy: never expose Python tracebacks or internal paths in API responses.
- [ ] 2.8 Write a half-page Security Decisions document — this will be pasted into the README in Phase 17.

---

## Phase 3 — MongoDB Setup (11 tasks)

- [ ] 3.1 Create a MongoDB Atlas cluster (free tier M0), whitelist your IP or use `0.0.0.0/0` for dev.
- [ ] 3.2 Create a production DB user with read/write permissions scoped to your database only.
- [ ] 3.3 Write Pydantic model for `User`: `id`, `email`, `hashed_password`, `created_at`.
- [ ] 3.4 Write Pydantic model for `Board`: `id`, `user_id`, `name`, `layout` (dict), `created_at`.
- [ ] 3.5 Write Pydantic model for `Widget`: `id`, `board_id`, `type`, `position`, `settings`.
- [ ] 3.6 Write Pydantic model for `Note`: `id`, `user_id`, `title`, `content_md`, `tags`, `linked_archive_ids`, `linked_event_ids`, `linked_form_ids`, `created_at`, `updated_at`.
- [ ] 3.7 Write Pydantic model for `ArchiveFile`: `id`, `user_id`, `filename`, `storage_path`, `mime_type`, `size_bytes`, `tags`, `linked_note_ids`, `created_at`, `updated_at`.
- [ ] 3.8 Write Pydantic model for `Event`: `id`, `user_id`, `title`, `start_time`, `end_time`, `description`, `tags`, `linked_note_ids`, `linked_form_ids`, `created_at`, `updated_at`.
- [ ] 3.9 Write Pydantic model for `Form`: `id`, `user_id`, `title`, `fields` (list of question dicts), `responses_history` (list), `tags`, `linked_note_ids`, `linked_event_ids`, `created_at`, `updated_at`.
- [ ] 3.10 Create indexes in Atlas or via Motor: `user_id` index on every collection; `tags` index on `note`, `archive_files`, `events`, `forms`.
- [ ] 3.11 Write a seed script: insert one document per collection, read it back, confirm it works.

---

## Phase 4 — Authentication (Backend) (13 tasks)

- [ ] 4.1 Create `POST /auth/register` — validate with Pydantic, check email uniqueness, hash password with passlib bcrypt, insert user.
- [ ] 4.2 Create `POST /auth/login` — find user by email, verify bcrypt hash, generate JWT on success.
- [ ] 4.3 Write JWT creation helper in `core/security.py` using `python-jose`.
- [ ] 4.4 Set JWT as httpOnly cookie in the login response: `response.set_cookie(httponly=True, secure=True, samesite='lax')`.
- [ ] 4.5 Create `get_current_user` as a FastAPI `Depends()` — reads cookie, decodes JWT, returns user.
- [ ] 4.6 Apply `Depends(get_current_user)` to all protected routers.
- [ ] 4.7 Create `POST /auth/logout` — deletes the auth cookie from the response.
- [ ] 4.8 Create `GET /auth/me` — returns current user info (used by frontend to check active session on load).
- [ ] 4.9 Test `POST /register` in Swagger (`/docs`) — confirm user appears in Atlas with `hashed_password`, not plaintext.
- [ ] 4.10 Test `POST /login` with correct credentials — confirm cookie is set in browser.
- [ ] 4.11 Test `POST /login` with wrong password — confirm 401 with message `"Invalid credentials"` only.
- [ ] 4.12 Test `GET /notes` (or any protected route) without cookie — confirm 401.
- [ ] 4.13 Test a protected route with a valid session — confirm 200.

---

## Phase 5 — Security Implementation (9 tasks)

- [ ] 5.1 Add `CORSMiddleware` to the FastAPI app with `allow_origins` sourced from `.env` (no wildcard).
- [ ] 5.2 Set up `slowapi` `Limiter` on the app instance; apply `@limiter.limit('5/minute')` to `POST /auth/login`.
- [ ] 5.3 Apply rate limiting to the file upload endpoint.
- [ ] 5.4 Implement file upload security: reject non-allowlisted MIME types with 400, enforce max file size, save files with `uuid4` filenames.
- [ ] 5.5 Install `bleach`; sanitize all markdown content before saving to the database.
- [ ] 5.6 Add a global exception handler (`@app.exception_handler(Exception)`) returning clean JSON with no tracebacks.
- [ ] 5.7 Add a request body size limit (via uvicorn config or middleware, e.g. 10 MB cap).
- [ ] 5.8 Verify `.env` is never committed: `git log --all -- .env` should return nothing.
- [ ] 5.9 For production settings: set `debug=False`, `secure=True` on cookies, disable `/docs` and `/redoc`.

---

## Phase 6 — Authentication (Frontend) (12 tasks)

- [ ] 6.1 Create `/register` page with email and password fields — use `onClick` handlers, not HTML form submit.
- [ ] 6.2 Create `/login` page.
- [ ] 6.3 Create `AuthContext` (or Zustand store) to hold current user and auth loading state.
- [ ] 6.4 On app startup, call `GET /auth/me` to check for a valid existing cookie session.
- [ ] 6.5 Wire Register form to `POST /auth/register` — redirect to `/login` on success, show error on failure.
- [ ] 6.6 Wire Login form to `POST /auth/login` — update auth context, redirect to dashboard on success.
- [ ] 6.7 Create `ProtectedRoute` component that redirects to `/login` if user is null.
- [ ] 6.8 Wrap all dashboard routes in `ProtectedRoute`.
- [ ] 6.9 Add a Logout button that calls `POST /auth/logout` and clears the auth context.
- [ ] 6.10 Show a loading spinner during form submission.
- [ ] 6.11 Display API error messages below the relevant form field.
- [ ] 6.12 Test full flow: register → login → dashboard → logout → dashboard redirects to `/login`.

---

## Phase 7 — Dashboard Layout Engine (15 tasks)

- [ ] 7.1 Create the `Dashboard` page component.
- [ ] 7.2 Add `react-grid-layout` — render 2–3 placeholder boxes and confirm drag and resize work.
- [ ] 7.3 Create `WidgetWrapper` component: card shell with header (type icon, title, settings icon, remove button).
- [ ] 7.4 Create a widget type registry: an object mapping type string to React component.
- [ ] 7.5 Create an "Add Widget" button that opens a modal listing all four widget types with descriptions.
- [ ] 7.6 Clicking a widget type in the modal adds it to the grid at a default position.
- [ ] 7.7 Create `GET /boards/{id}/widgets` endpoint.
- [ ] 7.8 Create `POST /boards/{id}/widgets` endpoint (type, initial position/settings).
- [ ] 7.9 Create `PATCH /widgets/{id}` endpoint (position and/or settings update).
- [ ] 7.10 Create `DELETE /widgets/{id}` endpoint.
- [ ] 7.11 Wire Dashboard to load layout from API on mount.
- [ ] 7.12 Wire drag/resize stop event to call `PATCH /widgets/{id}`.
- [ ] 7.13 Wire "Add Widget" confirmation to `POST /boards/{id}/widgets`.
- [ ] 7.14 Wire remove button in `WidgetWrapper` to `DELETE /widgets/{id}`.
- [ ] 7.15 Test: add widgets → drag/resize → refresh → layout is restored exactly.

---

## Phase 8 — Note Widget (14 tasks)

- [ ] 8.1 Create `GET /notes` endpoint (all notes for current user, sorted by `updated_at` desc).
- [ ] 8.2 Create `POST /notes` endpoint (title, content_md, tags).
- [ ] 8.3 Create `GET /notes/{id}` endpoint.
- [ ] 8.4 Create `PATCH /notes/{id}` endpoint (title, content, tags, linked IDs).
- [ ] 8.5 Create `DELETE /notes/{id}` endpoint.
- [ ] 8.6 Install a markdown editor library (`@uiw/react-md-editor` or `react-simplemde-editor`).
- [ ] 8.7 Build Note widget — catalog/carousel mode: scrollable list of note cards.
- [ ] 8.8 Build Note widget — single note mode: full note rendered as markdown preview.
- [ ] 8.9 Add "New Note" button that opens the note editor view.
- [ ] 8.10 Add markdown preview toggle (edit mode ↔ preview mode).
- [ ] 8.11 Add tag input: type and press Enter to add a tag; click × to remove.
- [ ] 8.12 Apply the first tag's color as an accent on the note card header.
- [ ] 8.13 Add delete note with a confirmation step.
- [ ] 8.14 Make single-note vs catalog mode a switchable widget setting.

---

## Phase 9 — Archive Widget (15 tasks)

- [ ] 9.1 Create `POST /archive/upload` — accept `multipart/form-data`, validate MIME and size, store file, return metadata.
- [ ] 9.2 Create `GET /archive` endpoint (all files for user, with optional tags filter).
- [ ] 9.3 Create `GET /archive/{id}` endpoint.
- [ ] 9.4 Create `GET /archive/{id}/download` endpoint — serve file as a download response.
- [ ] 9.5 Create `PATCH /archive/{id}` endpoint (rename, update tags, update `linked_note_ids`).
- [ ] 9.6 Create `DELETE /archive/{id}` — delete from storage and remove the DB document.
- [ ] 9.7 Build Archive widget — table view: filename, type icon, size, tags, uploaded date, action buttons.
- [ ] 9.8 Build Archive widget — gallery view for image files (thumbnail grid).
- [ ] 9.9 Add file upload UI: drag-and-drop zone with click-to-browse fallback.
- [ ] 9.10 Show upload progress bar.
- [ ] 9.11 Add tag input on each uploaded file.
- [ ] 9.12 Add a download button per file.
- [ ] 9.13 Add delete with confirmation.
- [ ] 9.14 Show file type icon based on MIME type (pdf, image, video, text, etc.).
- [ ] 9.15 Add "Link to Note" action: opens note selector, updates `linked_note_ids` on the archive entry.

---

## Phase 10 — Calendar Widget (14 tasks)

- [ ] 10.1 Create `GET /events` endpoint (filter by `start`/`end` date range query params).
- [ ] 10.2 Create `POST /events` endpoint (title, start_time, end_time, description, tags).
- [ ] 10.3 Create `GET /events/{id}` endpoint.
- [ ] 10.4 Create `PATCH /events/{id}` endpoint.
- [ ] 10.5 Create `DELETE /events/{id}` endpoint.
- [ ] 10.6 Research and install a calendar library (`react-big-calendar` or `@fullcalendar/react`).
- [ ] 10.7 Build Calendar widget — month view showing event chips on their dates.
- [ ] 10.8 Build day view: click a day to see a list of that day's events.
- [ ] 10.9 Build event create/edit modal: title, start datetime, end datetime, description, tags.
- [ ] 10.10 Add click on empty slot → pre-fills the date in the create modal.
- [ ] 10.11 Add event deletion inside the edit modal.
- [ ] 10.12 Apply the first tag's color to the event chip on the calendar.
- [ ] 10.13 Build catalog/carousel mode: scrollable upcoming events list.
- [ ] 10.14 Add "Link to Note" and "Link to Form" actions inside the event detail view.

---

## Phase 11 — Form Widget (15 tasks)

- [ ] 11.1 Create `GET /forms` endpoint (all forms for user).
- [ ] 11.2 Create `POST /forms` endpoint (title, fields/questions list, tags).
- [ ] 11.3 Create `GET /forms/{id}` endpoint.
- [ ] 11.4 Create `PATCH /forms/{id}` endpoint.
- [ ] 11.5 Create `DELETE /forms/{id}` endpoint.
- [ ] 11.6 Create `POST /forms/{id}/responses` — saves a completed response to the form's history.
- [ ] 11.7 Create `GET /forms/{id}/responses` — returns full response history.
- [ ] 11.8 Build form builder UI: add/remove/reorder questions (multiple choice + short answer types).
- [ ] 11.9 Build form-taking view: renders each field with the appropriate input type.
- [ ] 11.10 Show score/result screen immediately after submission for quiz-type forms.
- [ ] 11.11 Show response history list (date + score/summary) below each form.
- [ ] 11.12 Build Form widget — table view: list of forms with last taken date and score.
- [ ] 11.13 Build Form widget — catalog/carousel view: form cards.
- [ ] 11.14 Add tag input to form creation.
- [ ] 11.15 Add "Link to Note" and "Link to Event" actions inside form detail view.

---

## Phase 12 — Tags + Relations System (16 tasks)

- [ ] 12.1 Build a reusable `TagInput` component used across all four widgets.
- [ ] 12.2 Confirm the first tag's color value is used as the widget header accent in `WidgetWrapper`.
- [ ] 12.3 Build a `TagFilterBar` component: row of clickable tag chips that toggle a filter.
- [ ] 12.4 Wire `TagFilterBar` in Note widget to `GET /notes?tags=...` query param.
- [ ] 12.5 Wire `TagFilterBar` in Archive, Calendar, and Form widgets to their respective filter params.
- [ ] 12.6 Build a `RelationPicker` component: searchable dropdown of documents from a given collection.
- [ ] 12.7 Wire `RelationPicker` in Note editor → link Archive files (updates `note.linked_archive_ids`).
- [ ] 12.8 Wire `RelationPicker` in Note editor → link Calendar events (`linked_event_ids`).
- [ ] 12.9 Wire `RelationPicker` in Note editor → link Forms (`linked_form_ids`).
- [ ] 12.10 Wire `RelationPicker` in Archive entry → link Notes.
- [ ] 12.11 Wire `RelationPicker` in Calendar event detail → link Notes and Forms.
- [ ] 12.12 Wire `RelationPicker` in Form detail → link Notes and Calendar events.
- [ ] 12.13 In Note detail view: show chips/preview cards for each linked archive file, event, and form.
- [ ] 12.14 In Archive entry detail: show linked notes.
- [ ] 12.15 In Calendar event detail: show linked notes and forms.
- [ ] 12.16 End-to-end test: Note → link Archive file → link Event → verify all three show each other.

---

## Phase 13 — UI / UX Polish (12 tasks)

- [ ] 13.1 Apply final color palette via Tailwind config (`extend.colors` with system tokens).
- [ ] 13.2 Apply consistent typography across all headings, body text, labels, and mono elements.
- [ ] 13.3 Add empty states to all four widgets: friendly icon and message for when there is no data.
- [ ] 13.4 Add loading skeletons or spinners to every widget while data is being fetched.
- [ ] 13.5 Install `react-hot-toast` or `sonner`; add toasts for every create, update, delete, and error action.
- [ ] 13.6 Review tab order on every form — a keyboard-only user should be able to navigate everything.
- [ ] 13.7 Check color contrast on all text (aim for WCAG AA: 4.5:1 for normal text).
- [ ] 13.8 Test layout at 1280px, 1024px, and 768px widths — fix obvious breakage.
- [ ] 13.9 Polish the login and register pages — first impression for the teacher.
- [ ] 13.10 Add a favicon and a meaningful browser tab title per page.
- [ ] 13.11 Add a smooth fade or scale transition when widgets are added/removed from the grid.
- [ ] 13.12 Ensure tag color accents work with both light and dark tag colors (check text legibility).

---

## Phase 14 — Error Handling (9 tasks)

- [ ] 14.1 Add a React `ErrorBoundary` wrapping the full app — render a friendly fallback UI on crash.
- [ ] 14.2 Create an Axios interceptor that catches 401 globally and redirects to `/login`.
- [ ] 14.3 Create an Axios interceptor that catches 5xx errors globally and fires an error toast.
- [ ] 14.4 Add frontend validation on every form: required fields, email format, min/max lengths — do not rely on backend alone.
- [ ] 14.5 Add a `/404` route with a friendly not-found page.
- [ ] 14.6 Simulate API failure in every widget — verify it fails gracefully without crashing the whole app.
- [ ] 14.7 In FastAPI: write a global `@app.exception_handler` that returns clean JSON with no traceback.
- [ ] 14.8 Confirm Pydantic validation errors (422) return human-readable field-level messages.
- [ ] 14.9 Test file upload edge cases: wrong type, file too large — confirm correct error message in UI.

---

## Phase 15 — Testing (11 tasks)

- [ ] 15.1 Install `pytest` and `httpx` in `/server` (`httpx` is required for FastAPI async test client).
- [ ] 15.2 Write test: `POST /auth/register` creates a user; password stored as hash, not plaintext.
- [ ] 15.3 Write test: `POST /auth/login` with correct password returns 200 and sets cookie.
- [ ] 15.4 Write test: `POST /auth/login` with wrong password returns 401.
- [ ] 15.5 Write test: `GET /notes` without auth cookie returns 401.
- [ ] 15.6 Write test: create two users; confirm user A cannot read user B's notes.
- [ ] 15.7 Repeat data isolation test for archive files, events, and forms.
- [ ] 15.8 Write test: file upload endpoint rejects a disallowed MIME type.
- [ ] 15.9 Write test: `GET /notes?tags=study` returns only notes tagged `study`.
- [ ] 15.10 Manual full-flow test: register → login → add all four widgets → populate data → drag layout → refresh → all data and layout persist → logout → login again.
- [ ] 15.11 Test in a second browser (Firefox or Safari if Chrome was used primarily).

---

## Phase 16 — Deployment (13 tasks)

- [ ] 16.1 Create a MongoDB Atlas production cluster (free M0 tier); create a production DB user.
- [ ] 16.2 Create a Render account; create a new Web Service pointed at `/server`.
- [ ] 16.3 Generate `requirements.txt`: `pip freeze > requirements.txt`.
- [ ] 16.4 Set all production env vars in Render: `MONGO_URI`, `SECRET_KEY`, `CORS_ORIGINS`, `ENV=production`.
- [ ] 16.5 Set Render start command: `uvicorn main:app --host 0.0.0.0 --port $PORT`.
- [ ] 16.6 Test all API endpoints against the live Render URL via Swagger (then disable `/docs` in production).
- [ ] 16.7 Create a Vercel account; deploy `/client`.
- [ ] 16.8 Set `VITE_API_URL` in Vercel env vars to your live Render URL.
- [ ] 16.9 Update `CORS_ORIGINS` in Render to include your Vercel domain.
- [ ] 16.10 Test file upload in production — confirm files are stored and downloadable (check storage path differences from local).
- [ ] 16.11 Open the live Vercel URL — perform the full register → use all widgets flow.
- [ ] 16.12 Confirm HTTPS is active on both Vercel and Render (automatic — verify the padlock).
- [ ] 16.13 Disable FastAPI `/docs` and `/redoc` in production (`docs_url=None`, `redoc_url=None`).

---

## Phase 17 — Documentation & Submission (11 tasks)

- [ ] 17.1 Clean up the Story Time section in the README — polish the grammar.
- [ ] 17.2 Write README tech stack section with a sentence on why each tool was chosen.
- [ ] 17.3 Write README local setup instructions: clone → venv → `pip install` → `.env` setup → uvicorn + vite.
- [ ] 17.4 Write README MongoDB collection overview (brief — not full Pydantic code).
- [ ] 17.5 Document all API endpoints: method, path, auth required, request body shape, response shape.
- [ ] 17.6 Write README Security Decisions section (paste from Phase 2 document).
- [ ] 17.7 Add the live demo link (Vercel URL) prominently at the top of the README.
- [ ] 17.8 Add screenshots of the dashboard, each of the four widgets, and the login page.
- [ ] 17.9 Write the project reflection for school: what was built, what was hardest, what would be done differently.
- [ ] 17.10 Final review: open the app fresh in an incognito window as a new user — check for anything broken or confusing.
- [ ] 17.11 Submit 🎉

---

## Summary Table

| Phase | Title | Tasks |
|-------|-------|-------|
| 0 | Planning & Design | 15 |
| 1 | Project Setup | 17 |
| 2 | Security Planning | 8 |
| 3 | MongoDB Setup | 11 |
| 4 | Authentication — Backend | 13 |
| 5 | Security Implementation | 9 |
| 6 | Authentication — Frontend | 12 |
| 7 | Dashboard Layout Engine | 15 |
| 8 | Note Widget | 14 |
| 9 | Archive Widget | 15 |
| 10 | Calendar Widget | 14 |
| 11 | Form Widget | 15 |
| 12 | Tags + Relations System | 16 |
| 13 | UI / UX Polish | 12 |
| 14 | Error Handling | 9 |
| 15 | Testing | 11 |
| 16 | Deployment | 13 |
| 17 | Documentation & Submission | 11 |
| **Total** | | **230** |

---

## Tips for Tracking

1. **Mark tasks complete** by changing `- [ ]` to `- [x]` as you finish them.
2. **Reference tasks by ID** in commit messages (e.g., "Phase 4, Task 3: Implement JWT helper").
3. **Use GitHub Projects** (optional) for visual Kanban tracking:
   - Go to your repo → Projects → New project
   - Create columns: `Backlog`, `In Progress`, `Review`, `Done`
   - Manually add or link issues to the project
4. **Weekly review**: Check this file once a week to ensure you're on track.

---

Good luck with your student dashboard build! 🚀
