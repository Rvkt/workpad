<%*
await tp.file.move("/Troubleshooting/" + tp.file.title)
tp.hooks.on_all_templates_executed(async () => {
	const file = tp.file.find_tfile(tp.file.path(true))
	await app.fileManager.processFrontMatter(file, (fm) => {
		fm.tags = (fm.tags || []).filter((t) => t !== "template")
	})
})
%>---
tags: [troubleshooting, template]
created: <% tp.date.now("YYYY-MM-DD") %>
---

## Problem
Describe the issue.

## Error
Include the exact error message, if applicable.

## Environment
- OS: 
- Framework: 
- Version: (app/dependency version)

## Investigation
Document what was checked.

## Solution
Document the verified solution or workaround.

## References
- Related notes: 
- External documentation: 
