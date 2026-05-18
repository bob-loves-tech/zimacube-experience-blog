# ZimaCube Blog — Design System

> Single source of truth for all visual and structural rules. Every HTML page, every generated component, and every Markdown source must follow this document. If it contradicts this file, it is wrong.

---

## 1. Philosophy

This blog is content-first. Design exists to make reading effortless, not to impress. The aesthetic is **intentionally restrained editorial** — warm paper, crisp typography, one accent color, generous whitespace. It should feel like a well-designed document, not a SaaS landing page.

**Core principles:**
- Typography does the heavy lifting
- One accent color only (purple)
- Warmth over sterility
- Motion is for function, not decoration
- Every element earns its place

---

## 2. Color Tokens

| Token | Hex / Value | Usage |
|-------|-------------|-------|
| `--bg-primary` | `#FAFAF8` | Page background (warm near-white) |
| `--bg-secondary` | `#F5F5F2` | Alternate sections, callout backgrounds |
| `--bg-code` | `#1E1E1E` | Code block background |
| `--text-primary` | `#1A1A1A` | Body text, headings |
| `--text-secondary` | `#6B6B6B` | Captions, meta, secondary text |
| `--text-muted` | `#9E9E9E` | Dates, footnotes, de-emphasized |
| `--accent` | `#6D28D9` | Links, active states, borders, bullets |
| `--accent-hover` | `#5B21B6` | Link hover, button hover |
| `--accent-tint` | `rgba(109, 40, 217, 0.06)` | Callout backgrounds, subtle highlights |
| `--border-light` | `#E5E5E5` | Image borders, dividers |
| `--border-accent` | `#6D28D9` | Blockquote left border, callout left border |

---

## 3. Typography

### Font Stacks

| Role | Stack | Fallback |
|------|-------|----------|
| Headings | `Cormorant Garamond` | `Georgia`, `Times New Roman`, serif |
| Body | `Inter` | `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, Roboto, sans-serif |
| Code | `JetBrains Mono` | `Fira Code`, `Consolas`, `Monaco`, monospace |

### Scale

| Element | Size | Weight | Line Height | Letter Spacing |
|---------|------|--------|-------------|----------------|
| `h1` (post title) | 2.5rem / 40px | 700 | 1.2 | -0.02em |
| `h2` (section) | 1.75rem / 28px | 600 | 1.3 | -0.01em |
| `h3` (subsection) | 1.25rem / 20px | 600 | 1.4 | 0 |
| Body | 1.125rem / 18px | 400 | 1.65 | 0 |
| Small / Caption | 0.875rem / 14px | 400 | 1.5 | 0 |
| Code | 0.9375rem / 15px | 400 | 1.6 | 0 |

**Rules:**
- Headings are serif. Body is sans-serif. No exceptions.
- Body text is always left-aligned. Never centered, never justified.
- Minimum body size: 16px on all screens.

---

## 4. Layout

### Content Area
- **Max width:** 720px for body text
- **Side padding:** 24px on mobile, 48px on tablet+
- **Centered** in viewport

### TOC Sidebar (Desktop 1024px+)
- **Width:** 260px
- **Position:** Sticky, left side
- **Behavior:** Collapsible via toggle button
- **Active state:** Purple left border + purple text for current section
- **Default:** Visible on load

### TOC Drawer (Mobile < 1024px)
- **Trigger:** Hamburger `☰` button top-right
- **Behavior:** Slides in from right, overlay with backdrop
- **Close:** `✕` button or backdrop click

### Breakpoints
| Name | Width | Behavior |
|------|-------|----------|
| Mobile | < 768px | Single column, TOC in drawer |
| Tablet | 768–1023px | Single column, TOC in drawer |
| Desktop | 1024px+ | Content + sticky sidebar |
| Large | 1440px+ | Same layout, more side margin |

---

## 5. Components

### Links
- **Default:** `--accent` color, no underline
- **Hover:** `--accent-hover`, underline appears
- **Visited:** Same as default (don't penalize readers)
- **Never:** default browser blue

### Blockquotes
- Left border: 3px solid `--accent`
- Background: `--accent-tint`
- Text: italic, `--text-primary`
- Padding: 16px 20px
- Margin: 24px 0

### Code Blocks
- Background: `--bg-code`
- Text: `#E4E4E4`
- Border radius: 4px
- Padding: 16px 20px
- Overflow-x: auto
- No language badge / label

### Inline Code
- Background: `#F0F0EE`
- Text: `--text-primary`
- Border radius: 3px
- Padding: 2px 6px
- Font: code stack

### Lists
- **Bullet:** Small purple square (8px)
- **Spacing:** 8px between items
- **Indent:** 24px from content edge

### Images
- Max width: 100% of content area
- Border radius: 4px
- Optional: 1px `--border-light` border
- Caption: `--text-secondary`, 0.875rem, centered below

### Callouts (Important Notes)
- Background: `--accent-tint`
- Left border: 3px solid `--accent`
- Padding: 16px 20px
- Border radius: 4px
- **No shadow**

### Date Footer
```
---
*Written: Month YYYY*
```
- Centered
- `--text-muted`
- 0.875rem
- Subtle top border: 1px `--border-light`
- Margin top: 48px

---

## 6. Heading Hierarchy (Strict)

This is **enforced** in both Markdown source and HTML output.

| Level | Usage | Count |
|-------|-------|-------|
| `#` | Post title **only** | Exactly 1 per file |
| `##` | Major sections | Unlimited |
| `###` | Subsections | Unlimited, but **must** be under a `##` |
| `####`+ | **Forbidden** | 0 |

**Rules:**
- No heading level skipping (`##` → `####` is invalid)
- No empty headings
- Headings must describe the content below, not decorate it
- Sentence case preferred ("Hardware overview" not "Hardware Overview")

---

## 7. DO This

✅ Use `--bg-primary` for all page backgrounds
✅ Use serif for headings, sans-serif for body
✅ Keep content column narrow (720px max) for readability
✅ Use purple (`--accent`) sparingly: links, active TOC, borders, bullets
✅ Add generous whitespace between sections (min 48px)
✅ Make the TOC sidebar sticky on desktop
✅ Use the hamburger drawer pattern on mobile
✅ Include backlinks at the bottom of every post
✅ Render the `---` + *Written date* footer on every post
✅ Left-align all body text
✅ Use blockquotes for asides and updates
✅ Use callouts for important notes that need to stand out
✅ Keep border radius at 4px or less
✅ Ensure all interactive elements have hover states
✅ Test at all breakpoints before considering done

---

## 8. NEVER Do This

❌ **Gradients** of any kind — no linear, no radial, no subtle fades
❌ **Glassmorphism / frosted glass** effects
❌ **Drop shadows** on cards, images, or containers
❌ **Rounded corners larger than 4px**
❌ **Default blue links** — always use `--accent` purple
❌ **AI slop**: glowing buttons, animated backgrounds, particle effects, cursor trails, gradient text
❌ **Sticky headers** that consume permanent screen space
❌ **Cookie banners, popups, modals, or interstitials**
❌ **Social media embed widgets, share buttons, like counters**
❌ **Emoji** in headings or UI chrome
❌ **Serif font for body text** — headings only
❌ **Centered body text** — always left-aligned
❌ **Justified text** — ragged right is more readable
❌ **All-caps headings** — sentence case or title case only
❌ **Decorative ornamental dividers** — use whitespace instead
❌ **Autoplaying media** of any kind
❌ **"Read time" badges** or estimated reading time
❌ **Tag clouds, category counts, or archive widgets**
❌ **Dark mode toggle** — single light theme, keep it simple
❌ **Massive hero images with text overlay**
❌ **Pagination within single posts**
❌ **Sidebar ads, promotional boxes, or newsletter signup forms**
❌ **"Related posts" carousels or grids**
❌ **Skip heading levels** (e.g., `##` straight to `####`)
❌ **Use `####` or deeper headings**
❌ **More than one `h1` per page**
❌ **Boldface everything** — bold is for genuine emphasis only
❌ **Excessive motion** — if it moves, it must serve a purpose

---

## 9. Backlinks Architecture

Every post HTML must include at the bottom:

### Related Posts (Outbound)
Links to posts this page references.

### Referenced By (Inbound)
Links to posts that reference this page.

**How generated:** Parse all `.md` files for relative links before HTML build. Build reverse index. Render both sections.

---

## 10. File Structure for Generated HTML

```
repo-root/
├── DESIGN.md                  # This file
├── README.md                  # GitHub repo index (unchanged)
├── index.md                   # Narrative homepage source
├── index.html                 # Generated homepage
├── .nojekyll                  # Disable Jekyll on GitHub Pages
├── posts/
│   ├── hardware/
│   │   ├── overview.md        # Source
│   │   ├── overview.html      # Generated
│   │   └── disassembly.md
│   ├── first-impressions/
│   │   ├── introduction.md
│   │   └── unboxing.md
│   └── ...
└── assets/
    └── images/
```

**Rule:** Every `.md` file in `posts/` has a corresponding `.html` file in the same folder.

---

## 11. GitHub Pages Setup

1. Add `.nojekyll` to repo root (prevents Jekyll processing)
2. Enable GitHub Pages from `main` branch, root folder
3. `index.html` is served as the homepage
4. All internal links use relative paths

---

*Last updated: May 2026*
