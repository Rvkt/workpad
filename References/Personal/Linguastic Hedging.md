<%*
if (!tp.file.folder(true).startsWith("05 Knowledge/Permanent Notes")) {
  await tp.file.move("05 Knowledge/Permanent Notes/" + tp.file.title);
}
-%>
---
type: permanent-note
created: <% tp.file.creation_date("YYYY-MM-DD") %>
status: evergreen
tags:
  - knowledge
  - zettelkasten
---


> [!knowledge] The Thesis
> State the single atomic insight concisely in your own words.

---

## 🔬 Argument & Supporting Evidence
Elaborate on the insight. Why is this universally true or actionable? What proof, architectural benchmark, or empirical reasoning supports it?

## 🌐 Context & Nuance
Where does this rule break down? What are the edge conditions?

## 🔗 Associative Links
- Origin Reference: 
- Contrasting Idea: 
- Supporting Mental Model: 
- Map of Content: 
