# Book to Frank

`book-to-frank` is a Codex skill for turning an accessible book into a parallel-reading edition inspired by Ilya Frank's method. It pairs original passages with translations, preserves the book's structure and images, and can prepare EPUB, Markdown, or PDF output.

## Install

### Install from this repository

Install the skill for your user account by cloning the repository into Codex's global skills folder:

```sh
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/Yurich84/book-to-frank.git "${CODEX_HOME:-$HOME/.codex}/skills/book-to-frank"
```

If `CODEX_HOME` is set, Codex uses that directory instead of `~/.codex`.

### Manual install

From the repository root, copy `SKILL.md` into the user-level skills folder:

```sh
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills/book-to-frank"
cp SKILL.md "${CODEX_HOME:-$HOME/.codex}/skills/book-to-frank/SKILL.md"
```

## Update the global install

If you installed by cloning the repository, update it from a terminal with:

```sh
git -C "${CODEX_HOME:-$HOME/.codex}/skills/book-to-frank" pull --ff-only origin main
```

If you installed manually, copy the newer `SKILL.md` over the installed file. Codex detects skill changes automatically; restart Codex if the updated version does not appear.

## Use

Invoke the skill with a link to an accessible book or attach the book file:

```text
$book-to-frank https://example.com/book
```

The skill offers selectable choices for pairing size (3–5 words, 5–10 words, sentences, or paragraphs), target language, and output format (EPUB, Markdown, or PDF) when the chat interface supports them. Otherwise, it presents a compact numbered menu. It then prepares ordered section files, processes each section with a separate agent when delegation is available, and assembles the final book. If the source has no title page, it requests one before generating the final output.

## Workflow notes

- The source must be accessible to the environment, either through the link or as an uploaded file.
- Generated working files and the final book are saved in the current project workspace unless the user specifies another location.
- Per-section agent delegation depends on the Codex environment. The skill asks before substituting sequential processing when delegation is unavailable.
