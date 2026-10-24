# Blog batch — 6 new Current Events posts + site-wide nav fix

Ready to drop into `SimonJSCProp/my-website`. The repo clone was not touched and no git
commands were run. Everything was built against the **live** site (fetched 24 Oct 2026),
not the stale local clone, so nothing here reverts an earlier change.

Two separate changes ship together:

1. **Six new Current Events posts.** 50 posts → 56. Current Events 12 → 18.
2. **The nav overflow fix**, applied to all 56 articles and `blog.html`.

Nothing is retired, so there are **no redirects and no `netlify.toml` change**.

---

## What to upload

### `blog/` — all 56 files

Upload the whole folder. Six are new posts; the other 50 are existing articles that
carry **only** the nav CSS fix, nothing else.

**New posts (6):**

| File | Read time |
|---|---|
| `blog/apra-debt-to-income-cap-2026.html` | 3 min |
| `blog/first-home-buyers-under-1-million-brisbane.html` | 4 min |
| `blog/lvr-above-80-refinancing-falling-values.html` | 4 min |
| `blog/2026-housing-downturn-vs-2022.html` | 4 min |
| `blog/queensland-budget-2026-27-investors.html` | 3 min |
| `blog/30-percent-minimum-tax-capital-gains.html` | 4 min |

All six are Current Events (`--cat-color: #ef4444`).

### Root — 2 files

| File | What changed |
|---|---|
| `blog.html` | 6 POSTS entries added; hero stat 50→56; banner "12 timely"→"18 timely"; `count-all` and results count 50→56; **plus the nav fix** |
| `sitemap.xml` | 6 blog URLs appended (68 URLs total, 56 of them blog) |

### Nothing to delete

---

## The nav fix

**The bug.** Every blog article overflowed horizontally between about 721px and 890px.
The nav only switched to its hamburger at 720px, but the logo plus seven links plus the
CTA need far more room than that. Tablets in portrait and small laptop windows got a
sideways scrollbar and a nav running off the edge.

**It was wider than the articles.** `blog.html` had the same fault (+68px at 721px), and
so do `services`, `about` and `contact` (+56px at 721px). `calculator` and
`portfolio-performance` are already clean.

**The site had a partial fix already.** `blog.html` carried an intermediate rule that
shrinks the nav between 721 and 900px:

```css
@media (max-width: 900px) {
  .nav-links { gap: 18px; }
  .nav-links a { font-size: 13px; }
}
```

Measured, that rule narrows the broken band but does not close it, which is why
`blog.html` was still overflowing. Two numbers in it were mistuned.

**What was applied.** The site's own rule, with both boundaries measured rather than
guessed:

```css
@media (max-width: 920px) {        /* shrink the nav */
  .nav-links { gap: 18px; }
  .nav-links a { font-size: 13px; }
}
@media (max-width: 840px) {        /* hamburger, was 720px */
  .hamburger { display: flex; }
  ...
}
```

Giving three clean bands:

| Viewport | Nav |
|---|---|
| ≤ 840px | Hamburger |
| 841 – 920px | Full nav, shrunk (18px gap, 13px links) |
| ≥ 921px | Full nav, normal (28px gap, 14px links) |

**Why 840 and 920 specifically.** The logo is 213px, the link row 537px, container padding
48px. Below 841px the logo and the first link collide (0px gap) and the links spill past
the container; below 921px the full-size nav does the same. Both numbers were measured at
the point the gap stays at a comfortable 27px or more, not estimated.

The earlier intuition that 900px would fix it was wrong in both directions: too low for the
full-size nav, and it left the hamburger threshold untouched, which was the actual fault.

**The diff per article is 5 lines and identical in all 56 files:**

```
-    @media (max-width: 720px) {
+    @media (max-width: 920px) {
+      .nav-links { gap: 18px; }
+      .nav-links a { font-size: 13px; }
+    }
+    @media (max-width: 840px) {
```

`blog.html` already had the rule, so there it is just two numbers: `900`→`920` and
`720`→`840`.

---

## What was verified locally

**Content**

- 56 articles on disk; `blog.html` renders 56 cards; no POSTS entry without a file and no
  file without a POSTS entry
- Filter counts: all 56, current-events 18, market-intel 12, buyers-agency 9, strategy 6,
  process 7, finance 4. The other five categories are untouched
- Hero stat 56, banner "Current Events: 18 timely articles", results count 56
- Card links are extensionless `/blog/<slug>`, matching the existing convention and each
  page's canonical
- Each new file: valid tag balance, exactly one `<h1>`, canonical == og:url == its own URL,
  `Article` + `FAQPage` JSON-LD both parse, read time present, references linkified in
  brand green
- `sitemap.xml` parses, 68 URLs, no duplicates, every `<loc>` resolves to a real file
- `blog.html` diffed against live: the only changes are the six POSTS entries, the four
  count numbers and the two nav numbers. No existing post was lost or altered
- The page JavaScript parses (`node --check`)

**Nav fix**

- All 56 articles plus `blog.html` swept at 721 / 780 / 840 / 841 / 900 / 921px:
  342 checks, zero overflow, zero container spill, no logo/nav collision
- Six representative pages swept at 30 widths from 320px to 1920px: 180 checks, all clean
- Boundary behaviour confirmed: hamburger at ≤840, shrunk nav 841–920, full nav ≥921
- Hamburger menu still opens at 840px and shows all seven links with no overflow
- All 56 re-validated after patching: tag balance, one `<h1>`, JSON-LD parses, canonical
  intact, nav/footer/GTM chrome intact, no stale 720px breakpoint left behind
- The diff against the live file is byte-identical in shape across all 56

---

## Two things to know

**`Rents.` is not bolded in `2026-housing-downturn-vs-2022`.** Under "What is the same?",
that paragraph opens with a lead-in word that reads like the bold lead-ins used elsewhere
in the same article, but it is not bold in the source .docx, so it was not bolded here.
Worth a quick look by the author if it was meant to match.

**One indentation tidy-up in `blog.html`.** The four entries added on 14 October were
indented two spaces deeper than the rest of the `POSTS` array. They are now normalised to
the file's own style. Whitespace only, no content change.

## Still outstanding

`services.html`, `about.html` and `contact.html` have the same nav overflow (+56px at
721px) and are **not fixed here**, because they are not part of this upload set and
touching them would widen it beyond the blog. They need the same two media queries.
`services` and `about` carry eight nav links rather than seven, so their boundaries should
be re-measured rather than copied from these files.
