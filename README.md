# Book to Frank

`book-to-frank` is an agent skill for turning an accessible book into a parallel-reading edition inspired by Ilya Frank's method. Its core instructions use the portable `SKILL.md` format and can be used with skill-compatible agents such as Codex and Claude. It pairs original passages with translations, preserves the book's structure and images, and can prepare EPUB, Markdown, or PDF output. Interface features and available tools depend on the host agent.

## Install

### Install with the skills CLI

From the project where you want to use the skill, run:

```sh
npx skills add Yurich84/book-to-frank -a codex -a claude-code
```

This installs it for Codex and Claude Code in the current project. Add `-g` to install it for your user account across projects:

```sh
npx skills add Yurich84/book-to-frank -g -a codex -a claude-code
```

The `skills` CLI supports other compatible agents too; see its [CLI documentation](https://github.com/vercel-labs/skills/blob/main/docs/commands.md) for agent names and options.

### Manual install

Alternatively, clone this repository into the skill directory used by your agent. For example, the user-level locations for Codex and Claude Code are:

```sh
# Codex, for all projects
git clone https://github.com/Yurich84/book-to-frank.git ~/.agents/skills/book-to-frank

# Claude Code, for all projects
git clone https://github.com/Yurich84/book-to-frank.git ~/.claude/skills/book-to-frank
```

For project-level use, clone into `.agents/skills/book-to-frank` for Codex or `.claude/skills/book-to-frank` for Claude Code.

## Update an installation

If you installed with the skills CLI, update it with:

```sh
npx skills update book-to-frank
```

If you installed by cloning the repository, update it from a terminal with:

```sh
git -C ~/.agents/skills/book-to-frank pull --ff-only origin main
```

If you installed manually, copy the newer `SKILL.md` over the installed file. Follow the host agent's instructions for refreshing its skill list.

## Use

Invoke the skill with a link to an accessible book or attach the book file:

```text
$book-to-frank https://example.com/book
```

The skill collects pairing size (3–5 words, 5–10 words, sentences, or paragraphs), target language, and output format (EPUB, Markdown, or PDF), using the host's choice UI when available or a compact numbered menu otherwise. It prepares ordered section files, uses separate agents when delegation is available, and otherwise processes sections sequentially. If the source has no title page, it requests one before generating the final output.

## Workflow notes

- The source must be accessible to the environment, either through the link or as an uploaded file.
- Generated working files and the final book are saved in the current project workspace unless the user specifies another location.
- Available tools, delegation, and interface features depend on the host agent.
