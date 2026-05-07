# 🎓 Student Dashboard App

## 🌍 Problem
Students use too many disconnected tools (notes, tests, calendars, tasks). They need **one place** to plan, study, and track progress — with widgets that can **talk to each other**.

## ✅ Solution
A **modular dashboard web app** where students add predefined widgets (Notes, Tests, Stats, Calendar, Tasks). Widgets are standardized in size but customizable, and **can connect** to show related data by tags or relations.

---

## ✨ Core Concept
- 🧩 Dashboard with draggable, resizable widgets  
- 🧱 Each widget is a reusable component  
- 🔗 Widgets connect via **tags + relations**  
- 👤 User accounts keep personal dashboards and data  

---

# 🧩 Widgets (Detailed Spec)

## 📝 Notes (File‑Based Knowledge)
**Purpose**  
Notes are external files (docx, pdf, png, etc.). The app **does not edit file contents** — only the metadata created by the app. Notes are the hub for connections to other widgets.

### Workflow  
- Single file rectangle → **File Viewer** (editable metadata)  
- Table of files rectangle → **File Manager** → File Viewer  
- Event viewer → File Manager (filtered by tag) → File Viewer  
- Event viewer → File Viewer (direct relation)  
- Task viewer → File Manager (filtered by tag) → File Viewer  
- Task viewer → File Viewer (direct relation)

### File Manager (Notes)
- Create / delete note entries  
- Upload or attach files  
- Bulk edit tags and relations  
- Filter by tag, date, type  
- Open File Viewer  

### File Viewer (Notes)
- View file (download/open; no in‑app editing in v1)  
- Edit metadata (title, tags, relations)  
- See all connections (tasks, events, forms, stats)

### Data Stored (Notes)
- Title  
- File reference (path / upload / mime type)  
- Tags  
- Relations to widgets  
- Created at / Updated at  

---

## 🗓️ Calendar / Events
**Purpose**  
Schedules study sessions, deadlines, and reminders. Events link to Notes and Tasks.

### Workflow  
- Calendar widget → **Event Viewer**  
- Event Viewer → linked Note (direct)  
- Event Viewer → File Manager (tag‑filtered)  
- Task → “Create Event” → Event Viewer  

### Event Viewer
- View event detail  
- Edit title, time, tags, relations  
- Jump to linked note/task  

### Data Stored (Events)
- Title  
- Start / End time  
- Tags  
- Description  
- Relations to Notes / Tasks / Forms  
- Created at / Updated at  

---

## ✅ Task Manager
**Purpose**  
A detailed to‑do system for study tasks and assignments. Tasks can link to Notes and be converted into events.

### Workflow  
- Task list widget → **Task Viewer**  
- Task Viewer → File Manager (tag‑filtered)  
- Task Viewer → File Viewer (direct relation)  
- Task Viewer → “Create Event” → Event Viewer  

### Task Manager (Table View)
- Create, edit, delete tasks  
- Bulk change status / tags  
- Filter by status, tag, due date  
- Open Task Viewer  

### Task Viewer
- Edit title, status, due date  
- Attach tags  
- Link to notes/forms  
- Convert task to event  

### Data Stored (Tasks)
- Title  
- Status (Not started / In progress / Done)  
- Due date + time  
- Tags  
- Relations to Notes / Events / Forms  
- Created at / Updated at  

---

## 🧪 Forms / Tests
**Purpose**  
Self‑testing tool with modular question types. Used for practice and stats.

### Workflow  
- Forms widget → **Forms Manager**  
- Forms Manager → **Form Viewer**  
- Form Viewer → Take Test → Results  
- Results → Stats widget (linked)  

### Forms Manager
- Create, edit, delete forms  
- Bulk edit tags / relations  
- Filter by tag, date, subject  
- Open Form Viewer  

### Form Viewer
- View and edit form structure  
- Start test  
- View results history  
- Edit metadata (tags, title, time limit, pass %)  

### Data Stored (Forms)
- Title  
- Questions & answers  
- Time limit  
- Required success %  
- Tags  
- Results history  
- Relations to Notes / Stats  
- Created at / Updated at  

---

## 📊 Stats
**Purpose**  
Visualizes progress and performance using data from Tasks or Forms.

### Workflow  
- Stats widget → **Stats Manager**  
- Stats Manager → **Stats Viewer**  
- Stats Viewer → source data (tasks/forms)  

### Stats Manager
- Create new stat cards  
- Select source widget (tasks/forms)  
- Choose tags + metrics  
- Manage existing stats  

### Stats Viewer
- Display chart (pie/bar/line)  
- Switch metric or tags  
- Jump to related tasks/forms  

### Data Stored (Stats)
- Source type (tasks/forms)  
- Selected tags  
- Metric type  
- Display type  
- Created at / Updated at  

---

## 🔔 Single Event Widget (Dashboard Preview)
**Purpose**  
Compact widget showing the next upcoming event or a pinned event.

### Workflow  
- Dashboard → Event Viewer  

### Data Stored
- Event ID  
- Display mode (next / pinned)  

---

# 🔗 Shared Concepts
**Tags**
- Used for filtering and linking  
- Created by users  
- First tag controls widget color  

**Relations**
- Notes ↔ Tasks  
- Notes ↔ Events  
- Notes ↔ Forms  
- Forms ↔ Stats  
- Tasks ↔ Events  

---

# ⚙️ Technical Decisions (Current)
- **One active account per session** (multi‑account switching can be added later)
- **Database storage** for all metadata
- **File uploads stored by the app** (with size limits in v1)
- **Notes are external files**; app only edits metadata
- **Relations stored in a single relations table** (no bi‑directional duplication)
- **Stats computed on open** (no live auto‑updates in background)
- **Forms v1 supports 3 question types**:  
  - True/False  
  - Single choice  
  - Multiple choice  
- **Task → Event is one‑way** (“Create Event” button)
- **Manager/Viewer views use shared templates** with type‑specific labels

---

Samuel Svoboda IT3 SŠPU
