# Book to Frank

`book-to-frank` is a Codex skill for turning an accessible book into a parallel-reading edition inspired by Ilya Frank's method. It pairs original passages with translations, preserves the book's structure and images, and can prepare EPUB, Markdown, or PDF output.

## Install

### Install from this repository

After the project is published on GitHub, replace `<repository-url>` with its clone URL:

```sh
git clone <repository-url> "$HOME/.codex/skills/book-to-frank"
```

If you already cloned this repository elsewhere, copy its `SKILL.md` into `~/.codex/skills/book-to-frank/`. Restart or refresh Codex if the new skill does not appear.

### Manual install

Create `~/.codex/skills/book-to-frank/` and copy the repository's `SKILL.md` there:

```text
~/.codex/skills/book-to-frank/SKILL.md
```

## Use

Invoke the skill with a link to an accessible book or attach the book file:

```text
$book-to-frank https://example.com/book
```

The skill asks how to pair source and translation (3–5 words, 5–10 words, sentences, or paragraphs), the target language, and the output format (EPUB, Markdown, or PDF). It then prepares ordered section files, processes each section with a separate agent when delegation is available, and assembles the final book. If the source has no title page, it requests one before generating the final output.

## Workflow notes

- The source must be accessible to the environment, either through the link or as an uploaded file.
- Generated working files and the final book are saved in the current project workspace unless the user specifies another location.
- Per-section agent delegation depends on the Codex environment. The skill asks before substituting sequential processing when delegation is unavailable.
