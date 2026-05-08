# 🎓 Student Dashboard App

## Story Time (skip for shorter summary)
As a student who always tried to enhance my study habits I always looked at the internet for the ✨**perfect**✨ study app. For some time I was okay with having simply my handwritten notes in my drawer and testing myself by hiding the words with my hand. I was doing this till I felt prepared for the test ahead. It's nice and simple, but with age came more work. Harder and longer assignments, tests and I needed to *upgrade*. I came upon [RemNote](https://www.remnote.com/). 

> Great app not only for testing yourself but also for storing, categorizing and managing knowledge. 

But then I needed some way to remind myself of tests on certain dates and I also wanted to keep track of what I have to do for school, what chores I had to do, what project tasks I needed done etc. So now I had **Google Calendar** and [Habitica](https://habitica.com/). As I went to study IT I became more interested in enhancing my studying ability's. I wanted to automate everything and I was switching from the holy trinity. It became annoying trying to connect everything into the perfect ecosystem and then still missing the mark in the end. I came close with [Notion](https://www.notion.com/) but there was still something bugging me about it.

> It was so much work to get my ideal digital study space. [Notion](https://www.notion.com/) had a lot of freedom but also so much limitations. It allowed me to do great things when I dig deep. But then I looked back and saw how much time I had to spend just organizing and thinking of my dashboard while making it pretty at the same time. Notion just missed the mark but was so close. 

Now while I was thinking about a final project for my school I was lost. Then my teacher gave me an idea of an app that would be the hub of tools for a student. 

>Everything a student needs in one place, one page. Simple, easy to use but handy tools that would make students life just that much easier.

Thats how I thought of 🎉***Students Dashboard***🎉

A web app, that would have the essential tools not only for studying but also for organizing yourself, your work and schedule, tasks and even visualizing your progress in graphs and others stats to keep track of your progress and keep you motivated! The goal is to have everything in one place and connected together. If you make yourself a test, take it a few times then you can add a stats widget and visualize your result to see how you're doing. You have a file you're studying from and don't remember the exact name? Look at the file manager, filter files by tag and then add the one important note onto the dashboard to avoid this petty process again!

The power of this app is that anything you want can be seen right there in one page and you can get anywhere with minimal effort while also making your study space pretty. You have the freedom of not only choosing what things you want to see but also how they should be shown. 

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
## Visual Example (not final design)
Made with AI

<img width="1200" height="900" alt="dashboard" src="https://github.com/user-attachments/assets/920c3e35-51bd-4c0e-8a7a-961ac8e2edbe" />

---

<img width="1200" height="900" alt="dashboard_modal" src="https://github.com/user-attachments/assets/0e8cc4e3-694d-4db7-95f3-237ac014711d" />

---
# 🧩 Widgets (Detailed Spec)

## 📝 Notes (File‑Based Knowledge)
**Purpose**  
Notes are external files (docx, pdf, png, etc.). The app **does not edit file contents** — only the metadata created by the app.

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

# 🗄️ Database Design (Lookup Table Version)
The schema uses lookup tables for types (item types, question types, task statuses, etc.) so new types can be added without changing the schema. Adding a new type = insert a new row into the lookup table, then update backend/frontend logic.

<img width="1984" height="1452" alt="Student Dashboard" src="https://github.com/user-attachments/assets/a427a7f4-6708-4e0f-811e-b52371548969" />

---
```dbml
Project student_dashboard {
  database_type: "PostgreSQL"
}

Table users {
  id uuid [pk]
  email varchar(254) [unique, not null]
  password_hash varchar(255) [not null]
  created_at timestamp [not null]

  indexes {
    (email) [unique]
  }
}

Table item_types {
  id uuid [pk]
  code varchar(20) [not null, unique] // note, task, event, form, stat
  label varchar(50) [not null]
  is_active boolean [not null, default: true]
}

Table relation_types {
  id uuid [pk]
  code varchar(20) [not null, unique] // related, reference, parent, child
  label varchar(50) [not null]
  is_active boolean [not null, default: true]
}

Table task_statuses {
  id uuid [pk]
  code varchar(20) [not null, unique] // not_started, in_progress, done
  label varchar(50) [not null]
  is_active boolean [not null, default: true]
}

Table question_types {
  id uuid [pk]
  code varchar(20) [not null, unique] // true_false, single_choice, multi_choice
  label varchar(50) [not null]
  is_active boolean [not null, default: true]
}

Table stats_source_types {
  id uuid [pk]
  code varchar(20) [not null, unique] // task, form
  label varchar(50) [not null]
  is_active boolean [not null, default: true]
}

Table display_types {
  id uuid [pk]
  code varchar(20) [not null, unique] // pie, bar, line
  label varchar(50) [not null]
  is_active boolean [not null, default: true]
}

Table items {
  id uuid [pk]
  user_id uuid [not null, ref: > users.id]
  type_id uuid [not null, ref: > item_types.id]
  title varchar(100) [not null]
  created_at timestamp [not null]
  updated_at timestamp [not null]

  indexes {
    (user_id)
    (type_id)
    (user_id, type_id)
    (created_at)
  }
}

Table tags {
  id uuid [pk]
  user_id uuid [not null, ref: > users.id]
  name varchar(50) [not null]
  color varchar(7) [not null]
  created_at timestamp [not null]

  indexes {
    (user_id)
    (user_id, name) [unique]
  }
}

Table item_tags {
  item_id uuid [not null, ref: > items.id]
  tag_id uuid [not null, ref: > tags.id]

  indexes {
    (item_id, tag_id) [unique]
    (tag_id)
  }
}

Table relations {
  id uuid [pk]
  from_id uuid [not null, ref: > items.id]
  to_id uuid [not null, ref: > items.id]
  relation_type_id uuid [not null, ref: > relation_types.id]
  created_at timestamp [not null]

  indexes {
    (from_id)
    (to_id)
    (from_id, to_id, relation_type_id) [unique]
  }
}

Table files {
  id uuid [pk]
  item_id uuid [not null, ref: > items.id]
  filename varchar(255) [not null]
  path varchar(500) [not null]
  mime_type varchar(100) [not null]
  size int [not null]
  created_at timestamp [not null]

  indexes {
    (item_id) [unique]
    (mime_type)
  }
}

Table task_fields {
  item_id uuid [pk, ref: > items.id]
  status_id uuid [not null, ref: > task_statuses.id]
  due_date timestamp

  indexes {
    (status_id)
    (due_date)
  }
}

Table event_fields {
  item_id uuid [pk, ref: > items.id]
  start_at timestamp [not null]
  end_at timestamp [not null]
  description text

  indexes {
    (start_at)
    (end_at)
  }
}

Table form_fields {
  item_id uuid [pk, ref: > items.id]
  time_limit int
  success_percent int

  indexes {
    (success_percent)
  }
}

Table form_questions {
  id uuid [pk]
  form_id uuid [not null, ref: > form_fields.item_id]
  type_id uuid [not null, ref: > question_types.id]
  prompt text [not null]
  data jsonb [not null]
  position int [not null]

  indexes {
    (form_id)
    (form_id, position) [unique]
    (type_id)
  }
}

Table form_results {
  id uuid [pk]
  form_id uuid [not null, ref: > form_fields.item_id]
  user_id uuid [not null, ref: > users.id]
  score_percent int [not null]
  answers jsonb [not null]
  created_at timestamp [not null]

  indexes {
    (form_id)
    (user_id)
    (form_id, user_id)
    (created_at)
  }
}

Table stats_fields {
  item_id uuid [pk, ref: > items.id]
  source_type_id uuid [not null, ref: > stats_source_types.id]
  metric_type varchar(50) [not null]
  display_type_id uuid [not null, ref: > display_types.id]
  config jsonb

  indexes {
    (source_type_id)
    (metric_type)
    (display_type_id)
  }
}
```

---

# 📚 Database Explanation

## ✅ Core Tables
- **users**: user accounts.
- **items**: central table for all widget items (notes, tasks, events, forms, stats). Every widget entry = one `items` row.

## ✅ Lookup Tables (Types)
These tables define allowed values and make the system extensible without schema changes:
- **item_types** (note, task, event, form, stat)
- **relation_types** (related, reference, parent, child)
- **task_statuses** (not_started, in_progress, done)
- **question_types** (true_false, single_choice, multi_choice)
- **stats_source_types** (task, form)
- **display_types** (pie, bar, line)

Add a new type by inserting a new row into the correct lookup table. The database accepts it without migrations.

## ✅ Tags
- **tags** store user-defined tags with color.
- **item_tags** is a many-to-many table connecting tags to items.

## ✅ Relations
- **relations** links any two items. Stored as a single row (no bi-directional duplication).
- To fetch all relations for an item, query where it appears as either `from_id` or `to_id`.

## ✅ Files (Notes)
- **files** stores uploaded files linked to note items (one file per note in v1).

## ✅ Task/Event Fields
- **task_fields** stores task-specific data (status, due date).
- **event_fields** stores event-specific data (start/end, description).

## ✅ Forms
- **form_fields** stores form metadata.
- **form_questions** stores question definitions (type + JSON data).
- **form_results** stores each test attempt (answers + score).

## ✅ Stats
- **stats_fields** stores how to compute a stat, not the computed data.
- The `config` JSON stores filters like tags, time range, or source IDs.
- Data is computed when the Stats Viewer is opened.

---

# 🔒 Input Validation (Outside the Database)
The database enforces types, lengths, and relationships, but inputs should also be validated before they reach the DB.

## ✅ General Validation Strategies
- **Schema validation**: strict schemas for each request body; reject unknown fields.
- **Regex validation**: enforce formats (email, HEX colors, filenames, allowed tag characters).
- **Length limits**: cap title/tag/description/prompt sizes before insert.
- **Enum/lookup validation**: verify type/status exists and is active.
- **Cross‑field rules**: end date after start date, positive time limits, score in range.
- **File checks**: MIME allowlist, size limits, filename sanitization, store with safe server‑side name.
- **HTML/JS sanitization**: strip scripts from any user‑generated text rendered in UI.
- **Rate limiting**: block abuse on uploads or repeated requests.

These checks keep invalid or malicious data out of the system even before the database layer.

---

Samuel Svoboda IT3 SŠPU
