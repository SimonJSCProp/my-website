# Blog batch — 2 new posts (6 November 2026)

Ready to drop into `SimonJSCProp/my-website`. Built from the **live** site (fetched
6 Nov 2026), so nothing here reverts an earlier change. No repo clone, no git commands.

Result: **56 posts → 58.** Current Events **18 → 19**, Finance & Tax **4 → 5**.
Nothing retired, so **no redirects and no `netlify.toml` change**.

---

## 1. Upload these 2 new files → `blog/`

| File | Category | Read |
|---|---|---|
| `blog/proposed-discretionary-trust-minimum-tax.html` | Current Events | 4 min |
| `blog/property-investor-cash-buffer.html` | Finance & Tax | 4 min |

## 2. Replace these 2 files in the repo root

| File | What changed |
|---|---|
| `blog.html` | 2 POSTS entries added; hero stat 56→58; banner "18 timely"→"19 timely"; `count-all` and results count 56→58 |
| `sitemap.xml` | 2 blog URLs appended (70 URLs total, 58 of them blog) |

## 3. Nothing to delete

---

## Categories came from the documents

Both .docx files now carry a `Category:` line in their metadata block, so the category
was taken from the author rather than inferred:

- Trust minimum tax → **Current Events** (`#ef4444`)
- Cash buffer → **Finance & Tax** (`#fb923c`)

## The cash buffer article contains a table

This is the first blog article on the site with one, so it needed table CSS that no
article template had. Rather than invent a style, it reuses the site's own: the
`.breakdown` table on `calculator.html`. Same structure (left label, right-aligned bold
amount, total row in brand green), retuned to the article body's typography.

The CSS is scoped to `.article-body` and is **only in the file that has a table** — the
trust article does not carry it.

```css
.article-body table { width: 100%; border-collapse: collapse; ... }
.article-body th    { uppercase, muted, border-bottom }
.article-body td:last-child { text-align: right; font-weight: 700; white-space: nowrap }
.article-body tr.total td:last-child { color: var(--green) }
```

On a 375px phone the labels wrap to two lines and the amounts stay on one, right-aligned.
Checked, not assumed.

## Template note

Both files were built from `apra-debt-to-income-cap-2026` and the Finance one recoloured,
rather than from an existing Finance article. The four existing Finance articles predate
the list/references/article-note CSS, so cloning one would have shipped an article whose
reference links render in raw browser blue.

---

## What was verified locally

- 58 articles on disk; `blog.html` renders 58 cards; no POSTS entry without a file and no
  file without a POSTS entry
- Filter counts: all 58, current-events 19, finance 5, market-intel 12, buyers-agency 9,
  strategy 6, process 7 — summing to 58. The four untouched categories are unchanged
- Hero stat 58, banner "Current Events: 19 timely articles", results count 58
- Card links are extensionless `/blog/<slug>`, matching the convention and each canonical
- Both files: valid tag balance, exactly one `<h1>`, canonical == og:url == own URL,
  `Article` + `FAQPage` JSON-LD both parse, `datePublished` 2026-11-06, correct category
  colour and chip, read time present, references linkified in brand green
- Both carry the 920/840 nav fix and no stale 720px breakpoint
- 51 checks across 17 widths from 320px to 1600px on both articles and the index: zero
  overflow, zero nav collisions, and the table never spills the article body
- `sitemap.xml` parses, 70 URLs, no duplicates
- `blog.html` diffed against live: only the two POSTS entries and the four count numbers.
  No existing post lost or altered
- The page JavaScript parses (`node --check`)

## Pre-existing, not introduced

Blog articles are clean across the full width range since the October nav fix. Nothing
outstanding on these two.
