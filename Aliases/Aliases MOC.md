---
type: moc
domain: alias
created: 2026-11-17
tags: [moc, alias]
---

## Overview
Index of all notes in `Aliases/`. Auto-generated via Dataview — add a note to this folder and it appears below.

```dataview
TABLE WITHOUT ID
  file.link AS "Note",
  created AS "Created"
FROM "Aliases"
WHERE file.name != "Aliases MOC"
SORT file.name ASC
```
