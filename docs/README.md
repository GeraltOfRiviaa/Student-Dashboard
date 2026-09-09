# 🎓 Student Dashboard App

> [!NOTE]
> **Updates:** The database architecture and API routes have been fully specified, featuring a dedicated master tag system to power UI autocomplete and visual styling[span_0](start_span)[span_0](end_span)[span_1](start_span)[span_1](end_span). See `citations.md` and `progress.md` in the [docs](/docs) folder[span_2](start_span)[span_2](end_span).

## 📖 Story Time
> [!TIP]
> This section is a personal backstory on why the project exists. Skip to [Problem](#-problem) for the short version.

As a student who always tried to enhance my study habits, I always looked across the internet for the ✨**perfect**✨ study app. For a long time, I was fine keeping handwritten notes in my drawer and testing myself by hiding key terms with my hand until I felt prepared. It was simple, but growing older meant harder assignments, longer tests, and an urgent need to *upgrade*. 

Eventually, I discovered [RemNote](https://www.remnote.com/)—a great tool not only for testing yourself, but also for storing and categorizing knowledge[span_3](start_span)[span_3](end_span). But soon, I needed a way to track upcoming test dates, school assignments, chores, and project milestones. That forced me to adopt **Google Calendar** and [Habitica](https://habitica.com/) alongside it[span_4](start_span)[span_4](end_span). 

When I began studying IT, my desire to automate and optimize my workflow grew[span_5](start_span)[span_5](end_span). Switching between this "holy trinity" of apps became frustrating; trying to stitch them into a single ecosystem always missed the mark. I came close with [Notion](https://www.notion.com/), but its infinite flexibility came with heavy friction—I spent more time organizing my workspace and tweaking layouts than actually studying[span_6](start_span)[span_6](end_span). Notion was remarkably close, but still fell short.

When searching for my final IT school project idea, my teacher suggested building a unified hub tailored specifically for students[span_7](start_span)[span_7](end_span). 

> Everything a student needs in one place, on a single page. Simple, highly effective tools that make academic life effortless.

That spark led to 🎉***Student Dashboard***🎉—a web application bringing together essential tools for studying, scheduling, task management, and progress tracking[span_8](start_span)[span_8](end_span). If you create a test and take it a few times, you can attach a stats widget to track your performance over time[span_9](start_span)[span_9](end_span). If you forget a file name, you can filter your archive by tag and pin the exact note directly to your dashboard[span_10](start_span)[span_10](end_span). You get total freedom over what you see and how it is displayed—all on one page[span_11](start_span)[span_11](end_span).

---

## 🌍 Problem
Students rely on too many disconnected tools (notes, files, calendar events, quizzes)[span_12](start_span)[span_12](end_span). They need **one central hub** to plan, study, and track progress—powered by widgets that can **talk to each other**[span_13](start_span)[span_13](end_span).

## ✅ Solution
A **modular dashboard web app** built with customizable, standardized widgets (Note, Archive, Calendar, Form)[span_14](start_span)[span_14](end_span). Widgets operate independently but **connect seamlessly** via shared tags or direct cross-item relations[span_15](start_span)[span_15](end_span).

---

## ✨ Core Concept
* 🧩 **Modular Dashboard:** Features draggable, resizable layout blocks[span_16](start_span)[span_16](end_span).
* 🧱 **Reusable Widgets:** Each tool acts as an isolated, reusable UI component[span_17](start_span)[span_17](end_span).
* 👤 **Isolated Accounts:** User authentication isolates personal dashboards and data[span_18](start_span)[span_18](end_span)[span_19](start_span)[span_19](end_span).

---

## 🖼️ Visual Example (Mockup Concept)
> [!NOTE]
> These wireframes illustrate the layout concept and do not represent final UI styling[span_20](start_span)[span_20](end_span).

<img width="1200" height="900" alt="dashboard" src="https://github.com/user-attachments/assets/920c3e35-51bd-4c0e-8a7a-961ac8e2edbe" />

---

<img width="1200" height="900" alt="dashboard_modal" src="https://github.com/user-attachments/assets/0e8cc4e3-694d-4db7-95f3-237ac014711d" />

---

# 🧩 Widgets (Detailed Spec)
All widgets support tag filtering and alternate display views (Single, Catalog, Table)[span_21](start_span)[span_21](end_span). The sections below focus on functionality unique to each widget type[span_22](start_span)[span_22](end_span).

## 📝 Note
### Summary
Plaintext and Markdown documents edited directly on the dashboard[span_23](start_span)[span_23](end_span). Notes support Single, Catalog, and Table presentation modes[span_24](start_span)[span_24](end_span).

### Actions
* Write and render rich Markdown (formatting, images, links)[span_25](start_span)[span_25](end_span).
* Link forms, calendar events, or attached files via metadata[span_26](start_span)[span_26](end_span).
* Attach files sourced from the Archive widget[span_27](start_span)[span_27](end_span).

### Data Stored
* **title:** String
* **content:** Markdown String[span_28](start_span)[span_28](end_span)
* **tags:** Array of Strings[span_29](start_span)[span_29](end_span)
* **created_at / updated_at:** Timestamps[span_30](start_span)[span_30](end_span)
* **user_id:** Reference ID[span_31](start_span)[span_31](end_span)

---

## 🗂️ Archive
### Summary
A central file manager widget for uploading, organizing, and attaching study documents (JPEG, PNG, PDF supported in v1)[span_32](start_span)[span_32](end_span).

### Actions
* Upload and download files[span_33](start_span)[span_33](end_span).
* Link files directly to notes or calendar events[span_34](start_span)[span_34](end_span).

### Data Stored
* **filename:** String[span_35](start_span)[span_35](end_span)
* **storage_path:** Internal storage reference path[span_36](start_span)[span_36](end_span)
* **mime_type / size:** File format and byte size metadata[span_37](start_span)[span_37](end_span)[span_38](start_span)[span_38](end_span)
* **tags:** Array of Strings[span_39](start_span)[span_39](end_span)
* **created_at / updated_at:** Timestamps[span_40](start_span)[span_40](end_span)
* **user_id:** Reference ID[span_41](start_span)[span_41](end_span)

---

## 🗓️ Calendar
### Summary
Displays scheduled events and reminders[span_42](start_span)[span_42](end_span). Calendar events link directly to study materials so users can jump straight into relevant notes or tests without searching[span_43](start_span)[span_43](end_span).

### Actions
* Create, edit, and view scheduled events[span_44](start_span)[span_44](end_span).
* Configure lead-time reminders ahead of scheduled dates[span_45](start_span)[span_45](end_span).
* Attach linked notes, forms, or archive files[span_46](start_span)[span_46](end_span).

### Data Stored
* **title:** String[span_47](start_span)[span_47](end_span)
* **description:** Plaintext details[span_48](start_span)[span_48](end_span)
* **start_time / end_time:** Datetime objects[span_49](start_span)[span_49](end_span)
* **reminders:** Array of lead times in minutes[span_50](start_span)[span_50](end_span)
* **tags:** Array of Strings[span_51](start_span)[span_51](end_span)
* **created_at / updated_at:** Timestamps[span_52](start_span)[span_52](end_span)
* **user_id:** Reference ID[span_53](start_span)[span_53](end_span)

---

## 🧪 Form
### Summary
Supports self-testing quizzes, practice exams, and structured data-collection forms[span_54](start_span)[span_54](end_span). Form submissions are isolated in a separate collection to prevent document bloat[span_55](start_span)[span_55](end_span).

### Actions
* Complete and submit quiz forms[span_56](start_span)[span_56](end_span).
* View historical submission results and test scores[span_57](start_span)[span_57](end_span).
* Link forms to corresponding notes or study events[span_58](start_span)[span_58](end_span).

### Data Stored
* **title:** String[span_59](start_span)[span_59](end_span)
* **fields:** Array of questions, field types, and answer keys[span_60](start_span)[span_60](end_span)
* **tags:** Array of Strings[span_61](start_span)[span_61](end_span)
* **created_at / updated_at:** Timestamps[span_62](start_span)[span_62](end_span)
* **user_id:** Reference ID[span_63](start_span)[span_63](end_span)

---

# ⚙️ Backend Structures

### ⚙️ Container
Every widget instance on the dashboard is wrapped by a **Container**—a layout block that stores positioning and saved filter criteria (`filter_tags`)[span_64](start_span)[span_64](end_span). Actual items (notes, files, events, forms) remain completely decoupled from containers[span_65](start_span)[span_65](end_span).

> [!WARNING]
> Container `type` (`note`, `archive`, `calendar`, `form`) is fixed at creation and cannot be changed afterward[span_66](start_span)[span_66](end_span)[span_67](start_span)[span_67](end_span).

* **type:** Fixed widget classification[span_68](start_span)[span_68](end_span)[span_69](start_span)[span_69](end_span)
* **title:** Container label string[span_70](start_span)[span_70](end_span)[span_71](start_span)[span_71](end_span)
* **filter_tags:** Array of strings used for database item queries[span_72](start_span)[span_72](end_span)[span_73](start_span)[span_73](end_span)
* **layout:** Position coordinates `{ x, y, w, h }`[span_74](start_span)[span_74](end_span)
* **user_id:** Reference ID[span_75](start_span)[span_75](end_span)[span_76](start_span)[span_76](end_span)
* **created_at / updated_at:** Timestamps[span_77](start_span)[span_77](end_span)

---

# 🔗 Shared Concepts

**Tags**
* Plain strings assigned directly to widget items and container filters[span_78](start_span)[span_78](end_span)[span_79](start_span)[span_79](end_span).
* Supported by a lightweight **Master Tags** collection for autocomplete, settings, and badge color customization[span_80](start_span)[span_80](end_span)[span_81](start_span)[span_81](end_span).

**Relations**
* Explicit connections stored in a centralized `links` collection to maintain a fully decoupled database schema[span_82](start_span)[span_82](end_span):
  * Notes ↔ Archive Files[span_83](start_span)[span_83](end_span)
  * Notes ↔ Calendar Events[span_84](start_span)[span_84](end_span)
  * Notes ↔ Forms[span_85](start_span)[span_85](end_span)
  * Forms ↔ Calendar Events[span_86](start_span)[span_86](end_span)

---

# ⚙️ Technical Decisions

> [!IMPORTANT]
> These represent core architecture decisions; open layout edge cases are tracked in `progress.md`[span_87](start_span)[span_87](end_span).

* **Single Session Scope:** One active account per session for v1[span_88](start_span)[span_88](end_span).
* **Local Storage:** App handles direct file storage with size limits[span_89](start_span)[span_89](end_span).
* **Decoupled Link Architecture:** Relationships live in an independent collection to prevent bidirectional sync bugs[span_90](start_span)[span_90](end_span).
* **Flexible View Modes:** Note, Archive, and Form support Table view; Note and Form support Catalog mode; Calendar supports Month/Day views[span_91](start_span)[span_91](end_span).
* **Immutable Containers:** Container types are fixed at instantiation[span_92](start_span)[span_92](end_span)[span_93](start_span)[span_93](end_span).

---

# 🧰 Tech Stack


---

# 🔒 Input Validation

Request bodies undergo validation prior to database execution[span_94](start_span)[span_94](end_span)[span_95](start_span)[span_95](end_span):

* **Schema Validation:** Enforce strict Pydantic schemas and reject unknown fields[span_96](start_span)[span_96](end_span).
* **Format Checking:** Enforce regex patterns on emails, hex color codes, and safe tag characters[span_97](start_span)[span_97](end_span).
* **Boundary Guardrails:** Enforce strict length limits on titles, tags, and text fields[span_98](start_span)[span_98](end_span).
* **File Protection:** Enforce MIME type allowlists (JPEG, PNG, PDF), file size limits, and filename sanitization[span_99](start_span)[span_99](end_span).
* **Data Sanitization:** Strip scripts from user content to prevent XSS attacks[span_100](start_span)[span_100](end_span).

---

# 📖 Database and API

The backend relies on **MongoDB** for its schema flexibility and **FastAPI** for automatic OpenAPI documentation and high-performance async execution[span_101](start_span)[span_101](end_span).

### 🗄️ Database Architecture

The application utilizes a non-relational database structure managed via MongoDB[span_102](start_span)[span_102](end_span). To maintain high performance and prevent data synchronization issues, collections are strictly decoupled—containers only store UI layouts and filter strings[span_103](start_span)[span_103](end_span), while cross-widget relationships are isolated in a dedicated links collection[span_104](start_span)[span_104](end_span).

---

#### 👤 Users
Stores authentication credentials and account settings[span_105](start_span)[span_105](end_span)[span_106](start_span)[span_106](end_span).
* **user_id:** Unique identifier for the account[span_107](start_span)[span_107](end_span)[span_108](start_span)[span_108](end_span).
* **email:** User login address (validated and unique)[span_109](start_span)[span_109](end_span).
* **password_hash:** Securely hashed password credential.
* **created_at / updated_at:** Timestamps tracking account lifecycle[span_110](start_span)[span_110](end_span).

---

#### ⚙️ Containers
Lives on the dashboard and represents a saved layout space and filter view[span_111](start_span)[span_111](end_span).
* **container_id:** Unique identifier for the container layout block.
* **user_id:** References the owning user account[span_112](start_span)[span_112](end_span)[span_113](start_span)[span_113](end_span).
* **title:** Custom display label set by the user[span_114](start_span)[span_114](end_span)[span_115](start_span)[span_115](end_span).
* **type:** Fixed widget type (`note`, `archive`, `calendar`, or `form`)[span_116](start_span)[span_116](end_span)[span_117](start_span)[span_117](end_span).
* **filter_tags:** Array of plain tag strings used to query items onto the container[span_118](start_span)[span_118](end_span)[span_119](start_span)[span_119](end_span).
* **layout:** Object containing position and sizing parameters `{ x, y, w, h }`[span_120](start_span)[span_120](end_span).
* **created_at / updated_at:** Creation and last-modified timestamps[span_121](start_span)[span_121](end_span).

---

#### 🏷️ Tags
Acts as a global lookup dictionary for UI autocompletion, settings management, and custom badge styling[span_122](start_span)[span_122](end_span)[span_123](start_span)[span_123](end_span).
* **tag_id:** Unique identifier for the tag entry.
* **user_id:** Isolates tags to the specific user account[span_124](start_span)[span_124](end_span)[span_125](start_span)[span_125](end_span).
* **name:** Plain text string matching the tag used across widgets[span_126](start_span)[span_126](end_span)[span_127](start_span)[span_127](end_span).
* **color:** Hex code value for visual UI tag badges[span_128](start_span)[span_128](end_span).
* **created_at / updated_at:** Creation and last-modified timestamps[span_129](start_span)[span_129](end_span).

---

#### 📝 Notes
Stores markdown documents edited directly within the dashboard[span_130](start_span)[span_130](end_span)[span_131](start_span)[span_131](end_span).
* **note_id:** Unique identifier for the note.
* **user_id:** References the owning user[span_132](start_span)[span_132](end_span)[span_133](start_span)[span_133](end_span).
* **title:** Plaintext note title[span_134](start_span)[span_134](end_span).
* **content:** Raw Markdown text body[span_135](start_span)[span_135](end_span)[span_136](start_span)[span_136](end_span).
* **tags:** Array of plain tag strings assigned to the note[span_137](start_span)[span_137](end_span)[span_138](start_span)[span_138](end_span).
* **created_at / updated_at:** Creation and edit timestamps[span_139](start_span)[span_139](end_span).

---

#### 🗂️ Archive
Tracks uploaded files and metadata[span_140](start_span)[span_140](end_span)[span_141](start_span)[span_141](end_span).
* **file_id:** Unique identifier for the archive item.
* **user_id:** References the owning user[span_142](start_span)[span_142](end_span)[span_143](start_span)[span_143](end_span).
* **filename:** Original upload file name[span_144](start_span)[span_144](end_span).
* **storage_path:** Internal server path where the file is stored[span_145](start_span)[span_145](end_span).
* **mime_type:** File format classification (JPEG, PNG, PDF)[span_146](start_span)[span_146](end_span).
* **size:** File size in bytes[span_147](start_span)[span_147](end_span).
* **tags:** Array of plain tag strings assigned to the file[span_148](start_span)[span_148](end_span)[span_149](start_span)[span_149](end_span).
* **created_at / updated_at:** Upload and modification timestamps[span_150](start_span)[span_150](end_span).

---

#### 🗓️ Calendar Events
Stores event reminders and scheduled tasks[span_151](start_span)[span_151](end_span)[span_152](start_span)[span_152](end_span).
* **event_id:** Unique identifier for the event.
* **user_id:** References the owning user[span_153](start_span)[span_153](end_span)[span_154](start_span)[span_154](end_span).
* **title:** Event title[span_155](start_span)[span_155](end_span).
* **description:** Detailed plaintext notes about the event[span_156](start_span)[span_156](end_span).
* **start_time / end_time:** Datetime objects for scheduling[span_157](start_span)[span_157](end_span).
* **reminders:** Array of lead times (in minutes) for notification triggers[span_158](start_span)[span_158](end_span)[span_159](start_span)[span_159](end_span).
* **tags:** Array of plain tag strings assigned to the event[span_160](start_span)[span_160](end_span)[span_161](start_span)[span_161](end_span).
* **created_at / updated_at:** Creation and edit timestamps[span_162](start_span)[span_162](end_span).

---

#### 🧪 Forms
Stores self-testing quizzes and data collection forms[span_163](start_span)[span_163](end_span)[span_164](start_span)[span_164](end_span).
* **form_id:** Unique identifier for the form template.
* **user_id:** References the owning user[span_165](start_span)[span_165](end_span)[span_166](start_span)[span_166](end_span).
* **title:** Form title[span_167](start_span)[span_167](end_span).
* **fields:** Structured array defining questions, input types, and correct answers[span_168](start_span)[span_168](end_span)[span_169](start_span)[span_169](end_span).
* **tags:** Array of plain tag strings assigned to the form[span_170](start_span)[span_170](end_span)[span_171](start_span)[span_171](end_span).
* **created_at / updated_at:** Creation and modification timestamps[span_172](start_span)[span_172](end_span).

---

#### 📊 Form Responses
Maintains user submission attempts decoupled from parent forms to prevent document bloat[span_173](start_span)[span_173](end_span)[span_174](start_span)[span_174](end_span).
* **response_id:** Unique identifier for the submission.
* **form_id:** References the parent Form document[span_175](start_span)[span_175](end_span).
* **user_id:** References the user who completed the form[span_176](start_span)[span_176](end_span).
* **answers:** Object or array holding the submitted responses[span_177](start_span)[span_177](end_span).
* **score / result:** Calculated completion percentage or test result[span_178](start_span)[span_178](end_span).
* **submitted_at:** Submission timestamp[span_179](start_span)[span_179](end_span).

---

#### 🔗 Links
Stores explicitly connected cross-widget relations[span_180](start_span)[span_180](end_span)[span_181](start_span)[span_181](end_span).
* **link_id:** Unique identifier for the relation entry.
* **user_id:** References the owning user account[span_182](start_span)[span_182](end_span).
* **item_a_id / item_a_type:** ID and collection type for the first connected item[span_183](start_span)[span_183](end_span).
* **item_b_id / item_b_type:** ID and collection type for the second connected item[span_184](start_span)[span_184](end_span).
* **created_at:** Timestamp when the link was created[span_185](start_span)[span_185](end_span).

---

### 🌐 Endpoints

#### 👤 Users
* `POST /users` — Register a new account[span_186](start_span)[span_186](end_span).
* `GET /users/{user_id}` — Retrieve profile data[span_187](start_span)[span_187](end_span).
* `PATCH /users/{user_id}` — Update user profile details[span_188](start_span)[span_188](end_span).
* `DELETE /users/{user_id}` — Delete user account[span_189](start_span)[span_189](end_span).
* `POST /auth/login` — Authenticate and retrieve access tokens[span_190](start_span)[span_190](end_span).

---

#### ⚙️ Containers
* `POST /containers` — Create a new dashboard container[span_191](start_span)[span_191](end_span).
* `GET /containers/{container_id}` — Retrieve a single container configuration[span_192](start_span)[span_192](end_span).
* `GET /users/{user_id}/containers` — Retrieve all active containers for a user[span_193](start_span)[span_193](end_span).
* `PATCH /containers/{container_id}` — Update container settings (title, layout, filterTags)[span_194](start_span)[span_194](end_span).
* `DELETE /containers/{container_id}` — Delete a container layout block[span_195](start_span)[span_195](end_span).

---

#### 🏷️ Tags
* `POST /tags` — Create a new master tag entry (name, color)[span_196](start_span)[span_196](end_span).
* `GET /tags` — Fetch all tags belonging to the authenticated user[span_197](start_span)[span_197](end_span).
* `GET /tags/autocomplete?query=` — Retrieve tag suggestions for UI dropdowns[span_198](start_span)[span_198](end_span).
* `PATCH /tags/{tag_id}` — Update tag metadata (e.g., color)[span_199](start_span)[span_199](end_span).
* `PUT /tags/{tag_id}/rename` — Rename a tag globally across the master collection and all tagged widget items[span_200](start_span)[span_200](end_span)[span_201](start_span)[span_201](end_span).
* `POST /tags/merge` — Merge two tags into one across all item collections[span_202](start_span)[span_202](end_span)[span_203](start_span)[span_203](end_span).
* `DELETE /tags/{tag_id}` — Remove a master tag entry[span_204](start_span)[span_204](end_span)[span_205](start_span)[span_205](end_span).

---

#### 🧩 Widgets
> `{widget_type}` represents `notes`, `archive`, `calendar-events`, or `forms`[span_206](start_span)[span_206](end_span).

* `POST /{widget_type}` — Create a new item[span_207](start_span)[span_207](end_span).
* `GET /{widget_type}/{widget_id}` — Retrieve a single item by ID[span_208](start_span)[span_208](end_span).
* `GET /{widget_type}?user_id=` — Fetch all items of a given type for a user[span_209](start_span)[span_209](end_span).
* `GET /{widget_type}?tags=math,bio` — Fetch items matching **any** specified tag[span_210](start_span)[span_210](end_span).
* `GET /{widget_type}?tags=math,bio&match=all` — Fetch items matching **all** specified tags[span_211](start_span)[span_211](end_span).
* `PATCH /{widget_type}/{widget_id}` — Update an existing item[span_212](start_span)[span_212](end_span).
* `DELETE /{widget_type}/{widget_id}` — Delete an item[span_213](start_span)[span_213](end_span).

---

#### 🖋️ Forms & Responses
* `POST /forms/{form_id}/responses` — Submit a completed form response[span_214](start_span)[span_214](end_span).
* `GET /forms/{form_id}/responses` — Fetch historical submission results for a form[span_215](start_span)[span_215](end_span).

---

#### 🔗 Links
* `POST /links` — Establish an explicit connection between two items[span_216](start_span)[span_216](end_span).
* `DELETE /links/{link_id}` — Remove an existing link[span_217](start_span)[span_217](end_span).
* `GET /links?item_id=` — Fetch all cross-widget relations for a given item[span_218](start_span)[span_218](end_span).

---

Samuel Svoboda | IT3 SŠPU[span_219](start_span)[span_219](end_span)