---
type: moc
domain: reference
created: 2026-11-17
tags: [moc, reference]
---

## Overview
Index of all notes in `References/`. Auto-generated via Dataview — add a note to this folder and it appears below.

```dataview
TABLE WITHOUT ID
  file.link AS "Note",
  created AS "Created"
FROM "References"
WHERE file.name != "References MOC"
SORT file.name ASC
```
