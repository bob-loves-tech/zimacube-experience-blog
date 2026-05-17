# AGENTS.md

## What this repo is

A personal Markdown blog/journal about the ZimaCube NAS. No build system, no tests, no CI — just `.md` files in a folder tree.

## Structure

```
posts/              ← all published content (topic-based subfolders)
assets/images/      ← photos and screenshots
_private/           ← gitignored: style guide, templates, workflow, consistency log
README.md           ← public index linking to all posts
```

## Critical: the private layer

`_private/` is in `.gitignore`. Agents working here **must** read these files before writing content:

| File | Purpose |
|------|---------|
| `_private/BLOG_STYLE_GUIDE.md` | Voice, tone, formatting, and anti-AI checklist |
| `_private/templates/new-post-workflow.md` | 7-phase process for creating posts |
| `_private/templates/post-draft-template.md` | Blank post scaffolding |
| `_private/consistency-log.md` | Cross-post fact tracking to prevent contradictions |
| `_private/post-ideas.md` | Topics the author wants written |

## Writing conventions

- **Voice**: Nicholas Cole style — simple words, short sentences, first-person, strong opinions, no AI filler
- **Post structure**: Starts with `# Title`, body sections with `## Headings`, ends with `---` then `*Written: Month YYYY*`
- **Cross-links**: Use relative paths (`../other-folder/post.md`)
- **Images**: Place in `assets/images/`, reference relatively from the post
- **No empty worksheets**: Posts must have actual content, not italicized question prompts

## Creating a new post

Follow the workflow in `_private/templates/new-post-workflow.md`:

1. Raw thought dump from the author
2. AI summarizes and asks clarifying questions
3. Check `_private/consistency-log.md` for contradictions
4. Draft using the template and style guide
5. Human review and approval
6. Commit + update consistency log
7. **Never push without explicit human approval** — ask first

Then update `README.md` to link the new post.

## Commits

- Short descriptive messages: "Write hardware overview: specs, storage, networking, and quirks"
- Branch: `main`
- Do not push unless the human explicitly asks
