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

## Navigation Bar

Every HTML page has a hardcoded top navigation bar. There is no build system to auto-generate it. When you add a new post or a new folder under `posts/`, you **must** update the nav block in every `.html` file.

### Current nav structure

The nav mirrors the folder tree inside `posts/`:

| Top-level link | Dropdown pages (files in that folder) |
|----------------|---------------------------------------|
| Home | `index.html` |
| First Impressions | `introduction.html`, `unboxing.html` |
| Hardware | `overview.html`, `disassembly.html`, `would-i-buy-it.html` |
| Windows Server | `bare-metal-setup.html` |
| Homelab Journal | `zimaos-review.html`, `proxmox-primary-os.html` |
| Meta | `disclaimer.html` |

### Adding a new post to an existing folder

1. Add the new page link inside the existing `<div class="dropdown">` for that folder in **every** `.html` file.
2. Remember: root pages use `posts/<folder>/<file>.html`. Post pages use `../<folder>/<file>.html`.

### Adding a brand-new section (new folder under `posts/`)

1. Create the new folder and add the post(s).
2. Add a new top-level `<li>` with a `<div class="dropdown">` inside, in the nav block of **every** `.html` file.
3. Update `README.md` and `index.html` to list the new section.

### Files that contain the nav block

- `index.html` (root-level links)
- Every file under `posts/**/*.html` (relative `../` links)

There are two identical nav templates — one for the root and one for posts. Update both, or copy-paste from an already-updated file.
