# 🎓 Student Dashboard App

## 🌍 Problem
Students use too many disconnected tools (notes, tests, calendars, tasks). They need **one place** to plan, study, and track progress — with widgets that can **talk to each other**.

## ✅ Solution
A **modular dashboard web app** where students add predefined widgets (Notes, Tests, Stats, Calendar, Tasks). Widgets are standardized in size but customizable, and **can connect** to show related data (e.g., Stats reads results from Tests, Notes link to Tests).

---

## ✨ Core Concept
- 🧩 Dashboard with draggable, resizable widgets  
- 🧱 Each widget is a reusable component  
- 🔗 Widgets can be connected by subject/tag relationships  
- 👤 User accounts keep personal dashboards and data  

---

## 🧩 MVP Widgets
- 📌 **Single event widget (from calendar)**
- 📝 **Notes widget** (text + file attachments)
- 🧪 **Tests / Forms widget** (create tests + save results)
- 📊 **Stats widget** (charts based on test results)
- 🗓️ **Calendar widget** (events + reminders)
- ✅ **Tasks widget** (to‑do list)

---

## 🧱 Architecture / Stack

### 🎨 Frontend
- ⚛️ **React** (widget components)
- ⚡ **Vite** (fast dev server + build)
- 💨 **Tailwind CSS** (quick styling)
- 🧲 **Grid/Drag Library** (e.g., react-grid-layout)

### 🛠️ Backend
- 🟢 **Node.js + Express**
- 🐘 **PostgreSQL**
- 🔁 REST API between frontend and backend

---

## 🔁 Data Flow
1. ⚛️ React requests data from Express API  
2. 🟢 Express reads/writes to PostgreSQL  
3. 🧩 Widgets render data and update UI  
4. 💾 Widget layout + settings saved per user  

---

## ✅ Checklist (What to Build)

### 1) Foundations 🏗️
- [ ] Create mono‑repo with `/client` and `/server`
- [ ] Initialize React app with Vite
- [ ] Create Express server with basic `/health` route
- [ ] Connect Postgres locally (test a simple query)

### 2) Database Setup 🗄️
- [ ] Design tables: `users`, `boards`, `widgets`, `notes`, `tests`, `test_results`, `events`, `tasks`
- [ ] Add `widget_settings` column (JSON) for per‑widget config
- [ ] Add foreign keys (e.g., widgets belong to board, board belongs to user)

### 3) Authentication (Concrete) 🔐
- [ ] `POST /auth/register` (create user, hash password)
- [ ] `POST /auth/login` (verify password, return token)
- [ ] Store JWT in browser (localStorage for MVP)
- [ ] Protect routes with middleware (must be logged in)

### 4) Dashboard & Layout 🧩
- [ ] Build grid layout with draggable/resizable widgets
- [ ] Save layout to database per user
- [ ] Load layout when user logs in

### 5) Widgets (MVP) 🧰
- [ ] Notes widget: create/edit note + file upload
- [ ] Tests widget: create test + save results
- [ ] Stats widget: show charts from test results
- [ ] Calendar widget: create/edit events
- [ ] Tasks widget: add/complete tasks

### 6) Widget Connections 🔗
- [ ] Add subject/tag fields to notes, tests, tasks
- [ ] Filter stats by subject/tag
- [ ] Link notes to tests

### 7) UI / UX 🎨
- [ ] Define colors + typography
- [ ] Create widget header style
- [ ] Add empty states (no data yet)
- [ ] Add loading states

### 8) Quality & Errors 🧪
- [ ] Validate all API inputs
- [ ] Return clear error messages
- [ ] Handle API failures in UI

### 9) Deployment (Free) 🚀
- [ ] Deploy frontend (Vercel/Netlify)
- [ ] Deploy backend (Render/Fly.io)
- [ ] Deploy Postgres (Render/Neon)

---

## 📝 Scope Note
Keep MVP focused. Advanced features (AI, Google Calendar sync, custom widgets) come only **after** core widgets are stable.
