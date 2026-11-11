---
name: book-to-frank
description: Convert an accessible book link or uploaded book into a parallel-reading edition in the style of Ilya Frank. Use when the user asks to prepare a book for language learning with source passages followed by translations.
---

# Book to Frank

Turn the supplied book into a parallel-reading edition: each original passage is followed immediately by its translation in the requested language, in *italic text inside parentheses*. Preserve the book's useful structure and illustrations, and deliver the requested EPUB, Markdown, or PDF.

## Start with the user's choices

Use the supplied link or attachment as the source. Check that it is accessible and identify its language, title page, main text, and available structure. Collect these three choices before processing:

1. **Pairing:** 3–5 words, 5–10 words, sentence by sentence, or paragraph by paragraph.
2. **Translation language:** suggest the language the user usually writes in during the conversation, when clear; allow another language.
3. **Output:** EPUB, Markdown, or PDF.

Present unanswered choices together in one compact interaction, using the host agent's available interaction features. If there is no structured choice UI, show a numbered menu and let the user answer in one line, such as `1) sentence 2) Ukrainian 3) EPUB`. Carry forward choices the user already gave, and ask only for missing ones. Ask about each choice only once; do not repeat a choice in a later message using different wording. If the user asks what a choice means, explain the options without asking for that choice again unless they still need to select it.

## Prepare the source

1. Extract the book's text and assets with tools suited to its format. For a web link, use the linked book only if its content can be accessed; if access is blocked, ask for an upload or accessible copy.
2. Identify the title page and the boundaries of the actual book text. Keep the title page as a separate source file or asset. Include literary content such as a preface or introduction when it belongs to the book. Exclude tables of contents, glossaries, indexes, publisher material, explanatory notes that are not part of the prose, and other supplementary matter at the beginning or end.
3. Preserve meaningful headings, bold, italics, paragraph breaks, and illustrations. Save each image locally with a stable relative path and retain its position/reference in the Markdown. Reflow text naturally: do not preserve line wrapping or hyphenation caused by the source page layout.
4. Split the main text into ordered Markdown files, preferably one per chapter or named section. When the source has no usable chapter or section divisions, split it into blocks of about 10 source pages. Keep headings and page order intact, and record the source page range for each block when available.
5. Save working files in a clear project directory, for example `source/`, `sections/`, `images/`, and `output/`. Keep the title page separate from the section files so it can be checked before assembly.

The preparation step is complete when all main-text content is represented once, in order, across the section files; excluded supplementary material is absent; and every referenced illustration resolves to a saved image.

## Translate each section

Process each section file with a separate worker agent when the host environment supports delegation. Give each worker only its assigned section plus the user's pairing size, target language, source language, and any shared terminology or names already established. If delegation is unavailable, process sections sequentially. Ask the worker or, when working directly, follow the same rules: preserve all source text and Markdown structure, and insert the translation immediately after each corresponding passage as *(*translated text*)* in italics. Preserve the source's paragraph boundaries and do not insert line breaks between sentences or sentence-translation pairs that belong to the same source paragraph. In sentence-by-sentence format, place each italicized translation directly after its source sentence on the same physical line, with no newline between the original sentence and its translation. In paragraph-by-paragraph format, put the full italicized translation in parentheses after the source paragraph, as a separate paragraph. For a passage-by-passage format, put the entire translation in parentheses and italics; do not italicize or parenthesize the original.

Run section workers independently when agent delegation is available. Each worker returns its completed section as a separate Markdown file, keeping the same filename and order. Keep a short shared glossary of names and recurring terms and pass updates to later workers. When working sequentially, maintain the same glossary and checks across sections. Describe delegation accurately; never imply that workers were used if the host does not support them.

After all workers finish, check every section for completeness and assembly readiness: all original passages remain, each has exactly one adjacent translation in the chosen language and format, section order and headings are preserved, and image links still resolve. Resolve omissions or inconsistent formatting with the responsible worker before assembling.

## Assemble and deliver

Before generating the final book, confirm that a title page exists. If the source has no title page, ask the user to upload one and pause final generation until it is available. Do not invent a title page or substitute a chapter heading.

Assemble the separate title page, translated sections in source order, and local images into the requested format:

- **Markdown:** deliver the assembled `.md` file and its image assets together, with working relative image links.
- **EPUB:** create a valid EPUB with the title page, section order, headings, inline formatting, and embedded illustrations intact.
- **PDF:** create a readable PDF with the title page, section order, headings, inline formatting, and illustrations intact.

Use available conversion tools such as Pandoc or another format-appropriate converter. If a requested format cannot be generated in the current environment, explain the missing capability and offer the closest usable intermediate files. Keep the deliverable focused on the book itself; do not add process notes, a generated table of contents, glossary, or other commentary to the book.

Completion means the requested-format file is present, the title page appears first, sections are in order, translations follow their matching source passages, and all illustrations are present.
