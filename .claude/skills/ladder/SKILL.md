---
name: ladder
description: Audit vertical (abstraction-depth) completeness of concept pages and fix top-heavy, bottom-heavy, or flat pages.
trigger: /ladder
---

# Ladder: Audit vertical completeness

The wiki's existing skills (ingest, digest, lint, graphify) are all **horizontal** — they link, propagate, cluster, and patch connections at the same abstraction level. None check whether a concept page can "go up" to higher abstractions or "go down" to concrete examples.

Based on the [[understanding-as-cloud]] framework: a page with only horizontal links but no vertical depth has a "flat cloud" — it's a definition, not understanding. Ladder audits and fixes the vertical axis.

## Usage

```
/ladder              — audit all concept pages, fix what's broken
/ladder <slug>       — audit and fix a single page (e.g. /ladder bounded-rationality)
/ladder --report     — audit only, no fixes
```

## Step 1 — Load wiki state

Read `wiki/index.md` and `wiki/home.md`. This is mandatory — classifying a page's UP direction depends on knowing what more-abstract pages exist in the wiki.

## Step 2 — Select pages to audit

Discover concept pages dynamically: scan `wiki/*.md` (files in the wiki root), excluding `home.md`, `index.md`, `log.md`, and anything in `wiki/sources/`. Source-summary pages have their own structure and are not subject to vertical completeness criteria.

If a `<slug>` was given, audit only that page.

If `--report` was given, set a flag to skip Step 4 (fixes).

## Step 3 — Classify each page

For each concept page, evaluate two axes:

### UP test — Can you ascend the ladder?

**Pass** if the page has at least one explicit upward connection:
- A wikilink to a MORE ABSTRACT concept WITH an explanatory sentence that frames the current concept as an instance, special case, or manifestation of the higher concept
- Examples that pass: "X is a special case of [[Y]]", "X exemplifies [[Y]]", "X is [[Y]]在产品维度的投射"
- The explanatory sentence is critical — a bare `[[something]]` in a link list does NOT count as upward

**Fail** if the page only has:
- Horizontal links (peer concepts at the same abstraction level)
- Downward links (to sources or more concrete pages)
- Bare wikilinks without explanatory sentences that establish a vertical relationship

### DOWN test — Can you descend the ladder?

**Pass** if the page has at least one concrete example that passes the Feynman test — could someone outside the domain grasp the concept through what's on this page? Any of these count:
- A named system, product, or organization (e.g., "AlphaGo", "Claude Code")
- A specific number or metric (e.g., "GPU prices rose 40%")
- A real-world scenario or case study (e.g., "Boris runs 30-minute loop reports")
- An everyday analogy grounded in common experience (e.g., "像给故障发动机镀金")
- A specific observation from a cited source (e.g., "Claude查时钟每15分钟一次")

**Fail** if the page only has:
- Abstract definitions or restatements of the concept
- Links to other abstract concepts
- Hypotheticals without specifics ("for example, if someone were to...")

### Classification matrix

| UP | DOWN | Class | Meaning |
|----|------|-------|---------|
| Yes | Yes | **Solid** | Full cloud shape — understanding is real |
| Yes | No | **Top-heavy** | High-level term with nothing concrete below |
| No | Yes | **Bottom-heavy** | Examples exist but no skyhook to higher principles |
| No | No | **Flat** | Only horizontal links, no vertical at all |

### Natural level adjustment

Not all pages sit at the same abstraction level. Apply judgment:

- **Concrete concepts** (the page IS a specific system, technique, or practice — its primary content is already grounded) should be evaluated mainly on UP. Don't penalize a ground-level page for not having even more concrete examples below it; it may itself be the example for something above.
- **Abstract concepts** (the page describes a principle, framework, or pattern — its TL;DR is an abstract claim) should be evaluated mainly on DOWN. The more abstract the page, the more critical concrete examples become.

### Bulk mode: subagent delegation

If auditing more than 15 pages, use subagents for classification. Group pages into chunks of 10-15. One subagent per chunk. Pass this rubric verbatim to each subagent so classifications stay consistent. The main thread summarizes and spot-checks a few results.

## Step 4 — Fix pages (skip if --report)

**Fix, don't just report.** Make surgical edits — add sections or sentences, do not rewrite existing content.

### Top-heavy (has UP, no DOWN)

Add concrete grounding:
- Check if any cited sources on the page contain concrete examples — if so, surface them
- Add a concrete example or analogy that passes the Feynman test
- If drawing from your own knowledge rather than a cited source, mark the example clearly with `(~)` to indicate it's an inference, not a wiki source claim
- Never invent specific numbers, named events, or quotations without a source

### Bottom-heavy (has DOWN, no UP)

Add upward connection:
- Identify the higher-level principle this concept exemplifies
- Check `wiki/index.md` for an existing page at that level — if it exists, add an explicit upward sentence with a wikilink
- If no suitable abstract page exists in the wiki, flag it as a gap in the report (the wiki may need a new abstract page) — do NOT create new pages without user approval

### Flat (neither UP nor DOWN)

Add both:
1. Upward link first (easier to identify the higher principle)
2. Then concrete examples

Prioritize by inbound link count — use `wiki/index.md` and grep for `[[slug]]` across the wiki to estimate. Pages with many inbound links but poor vertical structure are the worst failures: many readers arrive at them and find an incomplete cloud.

### Solid

No changes needed.

## Step 5 — Report

Present a classification table:

```
| Page | UP | DOWN | Class | Action |
|------|-----|------|-------|--------|
| intelligence-vs-wisdom | Yes | Yes | Solid | -- |
| loop-scheduling | Yes | Weak | Top-heavy | Added concrete examples |
| ... | ... | ... | ... | ... |
```

Then overall statistics:

```
Ladder audit: N concept pages
  Solid:        X (P%)
  Top-heavy:    X (P%)  ← most common gap
  Bottom-heavy: X (P%)
  Flat:         X (P%)

Fixed: X pages
Gaps: X pages need new abstract pages (flagged, not auto-created)
```

**Priority callouts**: Flag any page that is flat or top-heavy AND has high inbound link count. These are the most expensive gaps — many readers reach them and find an incomplete cloud.

**Cross-skill note**: After ladder adds concrete examples, suggest running `/lint` to catch new cross-link opportunities from the added content.

## Step 6 — Log

Append to `wiki/log.md`: `## [YYYY-MM-DD HH:MM] ladder | <summary>`

Summary should include: page counts by classification, number of pages fixed, any gaps flagged.

## Rules

- **Fix, don't just report** — ladder is not a passive audit tool
- **Surgical edits** — add sections/sentences, don't rewrite existing content
- **Never invent facts** — if no source covers an example, mark it `(~)` for inference
- **Source-summary pages are excluded** — they have their own structure dictated by ingest
- **Don't update `home.md`** unless the ladder run created new pages (rare — flag, don't auto-create)
- **Never hardcode page counts** — dynamically discover from the filesystem and `wiki/index.md`
- **Subagent consistency** — pass this rubric verbatim to every subagent; main thread spot-checks classifications
