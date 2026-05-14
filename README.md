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
Students use too many disconnected tools (notes, files, calendars, forms). They need **one place** to plan, study, and track progress — with widgets that can **talk to each other**.

## ✅ Solution
A **modular dashboard web app** where students add predefined widgets (Note, Archive, Calendar, Form). Widgets are standardized in size but customizable, and **can connect** to show related data by tags or relations.

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

## 📝 Note
### Summary
Notes are plaintext/markdown documents editable directly in the app. The Note widget can be used as a single note widget or as a catalog/carousel view.

### Workflow
- Note widget → single note view **or** note catalog/carousel
- Note view → edit markdown content + metadata
- Note view → attach/select files from Archive

### Data Stored
- Title
- Markdown content
- Tags
- Linked archive file IDs
- Created at / Updated at

---

## 🗂️ Archive
### Summary
Archive is the file manager widget for storing files and connecting them to notes.

### Workflow
- Archive widget → archive table/gallery
- Archive entry → upload/download/manage file metadata
- Archive entry → link/unlink file to notes

### Data Stored
- Filename
- File reference (storage path / MIME type / size)
- Tags
- Linked note IDs
- Created at / Updated at

---

## 🗓️ Calendar
### Summary
Calendar manages academic events, deadlines, and reminders, and links events to notes/forms when needed.

### Workflow
- Calendar widget → month / day / event views
- Calendar widget → event catalog/carousel
- Event item → open and edit event details

### Data Stored
- Title
- Start / End time
- Description
- Tags
- Linked note/form IDs
- Created at / Updated at

---

## 🧪 Form
### Summary
Form provides self-testing and structured input workflows, with support for table and catalog/carousel presentation modes.

### Workflow
- Form widget → table **or** catalog/carousel
- Form item → open form, fill/submit, view result/history
- Form item → link to related notes/calendar events

### Data Stored
- Title
- Form fields/questions
- Responses/results history
- Tags
- Linked note/calendar IDs
- Created at / Updated at

---

# 🔗 Shared Concepts
**Tags**
- Used for filtering and linking  
- Created by users  
- First tag controls widget color  

**Relations**
- Notes ↔ Archive files  
- Notes ↔ Calendar events  
- Notes ↔ Forms  
- Forms ↔ Calendar events  

---

# ⚙️ Technical Decisions (Current)
- **One active account per session** (multi‑account switching can be added later)
- **File uploads stored by the app** (with size limits in v1)
- **Note content is plaintext/markdown editable in app**
- **Archive files can be linked to notes**
- **Calendar supports month/day/event views**
- **Note, Form, and Calendar support catalog/carousel modes**
- **Note, Archive, and Form support table view**

---

# 🧰 Tech Stack
React + Tailwind  
        ↓  
FastAPI  
        ↓  
Pydantic  
        ↓  
MongoDB

---

# 🔒 Input Validation
Input should be validated before processing and persistence.

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
