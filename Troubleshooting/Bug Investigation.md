<%*
if (!tp.file.folder(true).startsWith("02 Work/Troubleshooting")) {
  await tp.file.move("02 Work/Troubleshooting/" + tp.file.title);
}
-%>
---
type: troubleshooting
created: <% tp.file.creation_date("YYYY-MM-DD") %>
status: resolved
severity: high
project: ""
tags:
  - bug
  - troubleshooting
---


> [!study] Issue Summary
> **Environment:** Production / Staging / Local
> **Component:** Flutter App / Django API / Database

---

## 💥 Symptom & Observed Behavior
What happened? Steps to reproduce.

## 🛑 Stack Trace / Error Logs
```text
{{error_log}}
```

## 🔬 Root Cause Analysis (RCA)
Why did this happen? Trace the execution flow or state mutation.

## 🛠️ The Permanent Fix
```python
# Code diff or solution
```

## 🛡️ Prevention & Guardrails
- [ ] Unit / Integration test added
- [ ] Technical documentation updated
