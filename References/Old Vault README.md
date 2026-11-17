# Knowledge Vault — Personal Second Brain

Structured Obsidian vault designed for full-stack engineering, continuous technical study, architectural decision records, and personal development. Built on an 8-domain color-coded Second Brain architecture.

---

## 8-Domain Architecture & Note Mapping

| Domain / Folder | Notes Held | Subfolders | Template (`99 System/Templates/`) | Primary Tags |
| :--- | :--- | :--- | :--- | :--- |
| **`00 Home/`** | Command center & live dashboards | — | — | `#dashboard`, `#home` |
| **`01 Daily Notes/`** | Daily cadences, weekly summaries, monthly reviews | `Daily/`<br>`Weekly/`<br>`Monthly/` | `Daily Note.md`<br>`Weekly Review.md`<br>`Monthly Review.md` | `#daily-note`<br>`#weekly-review`<br>`#monthly-review` |
| **`02 Work/`** | Professional engineering records, ADRs, logs, bugs | `Work Logs/`<br>`Meetings/`<br>`Decisions/`<br>`Troubleshooting/`<br>`Responsibilities/`<br>`Technical Documentation/` | `Work Log.md`<br>`Meeting Note.md`<br>`Decision Record.md`<br>`Bug Investigation.md` | `#worklog`<br>`#meeting`<br>`#decision`, `#adr`<br>`#bug`, `#troubleshooting` |
| **`03 Journal/`** | Reflections, introspections, state of mind | — | `Personal Journal.md` | `#journal`, `#reflection` |
| **`04 Projects & Goals/`** | Active projects, strategic OKRs, retrospectives | `Projects/`<br>`Goals/`<br>`Reviews/` | `Project Overview.md`<br>`Goal.md`<br>`Retrospective.md` | `#project`<br>`#goal`<br>`#retrospective` |
| **`05 Knowledge/`** | Atomic Zettelkasten notes, concepts, mental models, technical study | `Concepts/`<br>`Permanent Notes/`<br>`Mental Models/`<br>`Maps of Content/`<br>`Study/` | `Technical Concept.md`<br>`Permanent Knowledge Note.md`<br>`Programming Learning Note.md` | `#concept`<br>`#knowledge`, `#zettelkasten`<br>`#study`, `#moc` |
| **`06 Resources/`** | Book syntheses, external references, articles | `Books/`<br>`References/`<br>`Articles/`<br>`Documentation/` | `Book or Course Notes.md`<br>`Resource Reference.md` | `#resource`, `#book`<br>`#reference` |
| **`07 Archive/`** | Inactive projects, closed goals, deprecated notes | — | — | `#archive` |
| **`99 System/`** | Vault configurations, themes, templates, assets | `Templates/`<br>`CSS/`<br>`Configuration/`<br>`Attachments/` | — | `#system`, `#templates` |

---

## Template Automation & Behaviors

All templates reside in `99 System/Templates/` and leverage Obsidian's **Templater** plugin:

1. **Automatic Folder Routing**:
   - Every template includes an auto-move execution script:
     ```markdown
     <%*
     if (!tp.file.folder(true).startsWith("Target/Folder")) {
       await tp.file.move("Target/Folder/" + tp.file.title);
     }
     -%>
     ```
   - When a note is created (in `01 Inbox` or anywhere in the vault) and a template is applied, it automatically moves to its dedicated home folder without manual filing.
   - If created directly within its target folder, the check avoids redundant moves.

2. **Clean Title Handling**:
   - Templates rely on Obsidian's native **Show inline title** setting.
   - Hardcoded H1 title tags with `<% tp.file.title %>` are omitted from templates to prevent duplicate titles and avoid notes permanently getting stamped with `# Untitled`.

3. **Folder Templates**:
   - Templater's `folder_templates` configuration maps destination directories directly to their corresponding templates for instant scaffolding when creating files inside target folders.

---

## Central Dashboards

- **Home Dashboard (`00 Home/Home.md`)**: Visual command center with quick actions, active project cards, and recent note feeds via Dataview.
- **Bases Dashboard (`ORIGIN.base`)**: Vault-wide index and per-domain table views for rapid sorting and filtering.
