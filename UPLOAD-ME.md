# Blog batch — 3 new, 4 refreshed, 1 retired (13 November 2026)

Built from the **live** site (fetched 13 Nov 2026). No repo clone, no git commands.

Result: **58 posts → 60.**

| Category | Before | After |
|---|---|---|
| current-events | 19 | **19** (one in, one out) |
| finance | 5 | **6** |
| process | 7 | **8** |
| market-intel / buyers-agency / strategy | 12 / 9 / 6 | unchanged |

---

## 1. Upload `blog/` — 7 files

**3 new posts:**

| File | Category | Read |
|---|---|---|
| `blog/rba-cash-rate-november-2026.html` | Current Events | 3 min |
| `blog/fixed-or-variable-rising-rates.html` | Finance & Tax | 3 min |
| `blog/check-flood-risk-brisbane.html` | Process & Contracts | 4 min |

**4 existing posts refreshed to 4.85%** (replacements, not new URLs):

```
blog/apra-debt-to-income-cap-2026.html
blog/property-investor-cash-buffer.html
blog/2026-housing-downturn-vs-2022.html
blog/iran-war-inflation-australian-property.html
```

## 2. Replace in the repo root

| File | What changed |
|---|---|
| `blog.html` | 1 POSTS entry removed, 3 added; two cards retitled for the 4.85% refresh; hero stat and counts 58→60 |
| `sitemap.xml` | 1 blog URL removed, 3 added (72 URLs, 60 of them blog) |

## 3. Delete from `blog/`

```
blog/rba-cash-rate-september-2026.html
```

Leaving it live keeps a page saying the rate is 4.60% indexed and makes the redirect unreachable.

## 4. Add to `netlify.toml`

Above the `/*` 404 catch-all, with the three October redirects. `netlify.toml` is not
web-served, so this is the one file that could not be rebuilt from live — add it by hand:

```toml
[[redirects]]
  from = "/blog/rba-cash-rate-september-2026"
  to = "/blog/rba-cash-rate-november-2026"
  status = 301
  force = true
```

---

## The 4.85% refresh

The rate moved to 4.85% on 3 November, the fifth rise of 2026. Four live articles were
updated. This was **not a find-and-replace** — several of the stale figures were attributed
to sources, and restating a source's September finding as a November one would misrepresent
it. What was done in each case:

**`apra-debt-to-income-cap-2026`** — the heaviest edit, because 4.60% was in its title.
- Title, H1, meta, og/twitter and schema headline → 4.85%
- Body: "the cash rate has risen to 4.85%, after a fifth increase in November 2026 (Kane, 2026)"
- **Cotality's borrowing-capacity figure was dated, not rewritten.** It now reads "Cotality
  estimated in September 2026 that the four rate rises *to that point* had cut borrowing
  capacity by almost $90,000 … The November increase has cut it further." The $90,000 and
  the "four rises" stay attached to the September source that actually said them.
- The worked example was **recalculated**, not just relabelled. A 6.85% variable plus the
  3pp buffer gave a 9.85% assessment rate; after the November rise passed on in full that
  becomes 7.10% + 3pp = 10.10%. On a $900,000 loan over 30 years the repayment goes from
  about $7,800 to about **$7,960** a month, and from around 62% to around **64%** of a
  $150,000 gross income. Both figures recomputed and checked.
- The article's conclusion is unchanged and in fact stronger: serviceability still binds
  before the DTI cap does.

**`property-investor-cash-buffer`** — "a 4.60% cash rate" → "the cash rate at 4.85%". The
sentence on further rises now cites the November source. The September CBA reference was
replaced by Kane (2026), since it only supported the superseded figure.

**`2026-housing-downturn-vs-2022`** — more than a rate swap, because the article's framing
had aged.
- "Six months into the 2026 downturn, national values are 5.2% below their March peak"
  → "Seven months in … values were 5.2% below their March peak by September (Cotality,
  2026a) and fell a further 1.2% in October (Cuthbert, 2026)." The 5.2% stays pinned to the
  September source rather than being presented as current.
- "risen 1 percentage point … to 4.60%, the highest setting since late 2011" → "risen 1.25
  percentage points across five increases, reaching 4.85% in November, the highest setting
  since November 2008 (Kane, 2026)". The 2008 comparison replaces 2011 because 4.85% clears
  the 2011 peak.
- Brisbane's September fall now carries October's further 2.0% fall.
- Meta description no longer leads with the stale 5.2%.
- Two references that only supported the old figures were removed; Kane and Cuthbert added.

**`iran-war-inflation-australian-property`** — "raised the cash rate four times this year,
taking it to 4.60%" → "five times this year, taking it to 4.85% in November (Kane, 2026)",
with Kane added to the references.

All four have `dateModified` bumped to 2026-11-13. `datePublished` is unchanged, so the
original publication dates stay honest.

**Reference titles were never altered.** `Commonwealth Bank of Australia. (2026, September).
RBA raises official cash rate to 4.60% in fourth increase of 2026` is the real title of a
real article; where it was no longer supporting any claim it was removed, never edited.

## Why the September article was retired

`rba-cash-rate-september-2026` is built entirely around "4.60%, the fourth hike of 2026" —
title, premise and FAQ. The new article is its direct successor, so it gets a 301 rather
than a 404, as `rate-cut-era-over-2026-hikes` did in October. Current Events stays at 19.

## Category decisions

Both new non-RBA documents carried `Category: … (suggested)`.

- **Fixed or Variable → Finance & Tax**, as suggested.
- **Flood risk → Process & Contracts**, not the suggested Market Intelligence. It is a
  step-by-step pre-purchase due-diligence guide, which is what that category holds
  (`Underground Services`, `What Easements Are`, `The Insurance Quote Trick That Flags
  High-Risk Properties`). Its own Step 4 is "get an insurance quote before you sign".
  Your call, 13 Nov.

---

## What was verified locally

- 60 articles on disk; `blog.html` renders 60 cards; no POSTS entry without a file and none
  the other way
- Counts: all 60, current-events 19, finance 6, process 8, market-intel 12, buyers-agency 9,
  strategy 6 — summing to 60
- **No article or index card claims 4.60% anywhere.** Swept all 60 articles plus the index
- **Every index card title and description matches its article's `<h1>` and meta
  description exactly**, across all 7 changed files. Two cards had to be retitled to stay
  in step with the refresh
- **Citation integrity checked on all four refreshed articles**: every in-text citation
  resolves to a reference, every reference is cited, and each list is alphabetical
- The retired slug appears nowhere in `blog.html`, `sitemap.xml` or any article
- All 7 files: valid tag balance, one `<h1>`, canonical == og:url == own URL, both JSON-LD
  blocks parse, 920/840 nav fix present, no stale 720px breakpoint
- New files carry `datePublished` 2026-11-13 and correct category colours — Current Events
  `#ef4444`, Finance & Tax `#fb923c`, Process & Contracts `#a78bfa` — confirmed in-browser
- 96 responsive checks across the new and refreshed articles and the index, 320px to
  1600px: zero overflow, zero nav collisions
- `sitemap.xml` parses, 72 URLs, no duplicates
- The page JavaScript parses (`node --check`)

## After uploading

**Check the redirect.** `/blog/rba-cash-rate-september-2026` should 301 to the November
article. Netlify applies it; it cannot be tested locally.

**The sitemap is now 72 URLs.** Resubmitting in Search Console still needs Simon —
`support@` has no access to the property.
