<%*
await tp.file.move("/References/" + tp.file.title)
tp.hooks.on_all_templates_executed(async () => {
	const file = tp.file.find_tfile(tp.file.path(true))
	await app.fileManager.processFrontMatter(file, (fm) => {
		fm.tags = (fm.tags || []).filter((t) => t !== "template")
	})
})
%>---
tags: [reference, template]
created: <% tp.date.now("YYYY-MM-DD") %>
---

## Overview
Brief explanation.

## Details
Useful technical information.

## Examples
Practical examples.

## References
Related documentation and notes.
