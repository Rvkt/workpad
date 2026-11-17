<%*
await tp.file.move("/Aliases/" + tp.file.title)
tp.hooks.on_all_templates_executed(async () => {
	const file = tp.file.find_tfile(tp.file.path(true))
	await app.fileManager.processFrontMatter(file, (fm) => {
		fm.tags = (fm.tags || []).filter((t) => t !== "template")
	})
})
%>---
tags: [alias, template]
created: <% tp.date.now("YYYY-MM-DD") %>
---

## Purpose
What does this alias simplify?

## Alias
```bash
# Alias definition
```

## Setup
Where and how to configure it.

## Usage
Example invocation.
