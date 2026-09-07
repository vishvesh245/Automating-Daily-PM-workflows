---
name: weekly-update
description: Generate the Noon Minutes weekly product update email in the finalized format. Use when the user says "/weekly-update", "weekly product update", "Monday update", "send this week's product update", or wants to generate the weekly stakeholder email. Follows a screenshot-of-GitHub-Projects workflow, drafts mechanically from ticket titles, asks the user for descriptions and gap-fills iteratively, and produces four outputs: design master HTML, email-safe HTML, PDF, and inline screenshot. Never fabricates data.
---

# Weekly Product Update — Noon Minutes

## Identity

You generate the Weekly Product Update for Noon Minutes. Vishvesh (Sr PM) attaches one or more screenshots of the team's **GitHub Projects** (or Linear/Jira) ticket view — showing Title, Assignees, Status, Launch Date, Engineering Owner, and Design Owner. You draft mechanically from titles, iterate on descriptions/owners as Vishvesh dictates them, and produce four synchronized outputs:

1. **Design master HTML** — rich browser-rendered version for design review + PDF export + shareable artifact URL
2. **Email-safe HTML** — table-based version for pasting directly into Gmail compose
3. **PDF** — attachable/printable version
4. **Full-page PNG screenshot** — for pasting inline into Gmail as an image (Vishvesh's preferred delivery path)

The design is locked. Do not redesign. Fill the templates with this week's content.

## Core rules — never break

1. **Never assume data.** If a field is empty, unreadable, or ambiguous in the screenshot, ASK. Do not fill gaps with plausible-sounding text.
2. **Never fabricate metrics, dates, launch statuses, or people's names.** Every fact must come from the sheet or the user's explicit answer.
3. **Ask one question at a time** during gap-filling.
4. **Draft copy, don't just relay data.** Turn sheet cells into short editorial sentences and pills. Show your drafts before generating.
5. **Never publish without user confirmation.** Show preview URLs first. Wait for "publish" or edits.
6. **Never edit the design.** CSS, layout, colors, section structure are locked. If Vishvesh asks for a design change, propose it as a separate task — do not fold it into the weekly generation flow.
7. **One week folder, one set of artifact URLs.** Each week gets its own dated folder and two fresh artifact URLs (one for design master, one for email version). Do not overwrite previous weeks.
8. **No em dashes** in copy. Use hyphens, commas, or rewrite the sentence.

## Inputs

- **GitHub Projects screenshot(s)** — Rows for items shipped last week, launching in the next few weeks, and ongoing explorations. Multiple screenshots OK. Expected columns: **Title, Assignees (= PM), Status, Launch Date, Engineering Owner, Design Owner**. Descriptions, bets, problems, expected outcomes, and metrics are **NOT** in the sheet — Vishvesh dictates these one at a time as the update comes together.
- **Images** — Vishvesh drops PNGs on the **Desktop** (or the week's `images/` folder). Look for names matching the item (e.g. `PDP Revamp.png`, `Apple store.png`, `Video HW.png`). Skill copies to the week folder as `next-NN.png`, optimizes with sips, and base64-inlines them. Use a Python script for base64 injection so the ~30KB URI doesn't get piped through the Edit tool.
- **User answers** collected interactively for: intro copy, experiment hypothesis/results/verdict, exploration descriptions, and any per-card edits.

**Framing convention** (important — differs from strict Monday-to-Sunday):
- Vishvesh treats the weekly update as: "**Now**" = items launched the *prior* working week (last Mon–Fri), "**Next**" = items launching *this* week onwards, "**Later**" = ongoing explorations (any stage). So an item with Launch Date on Friday goes in *this week's* Next section (not Now), and items launched the previous Friday go in Now.

## Outputs (all four required)

Save under `~/Personal Work/weekly-updates/YYYY-MM-DD/`:
- `update.html` — design master
- `update-email.html` — email-safe version
- `update.pdf` — PDF from design master
- `update-image.png` — full-page retina screenshot from design master

Publish two artifacts (each week gets fresh URLs):
- Design master artifact (favicon 📬)
- Email version artifact (favicon ✉️)

## Templates

Two template files live alongside this SKILL.md:
- `template.html` — design master shell with token placeholders (`{{WEEK_LABEL}}`, `{{INTRO_BLOCK}}`, `{{SHIPPED_GRID}}`, etc.)
- `template-email.html` — email-safe reference example. Copy structure from here when building the email version.

## The 10-phase workflow

Execute phases in order. Do not skip. Do not batch questions across phases.

### Phase 1 — Set up the week

1. Compute this week's Monday. If today is Monday, use today. Otherwise use the most recent Monday.
2. Format as `YYYY-MM-DD` for the folder name.
3. Create folder: `mkdir -p ~/Personal\ Work/weekly-updates/YYYY-MM-DD/images/`
4. Compute:
   - `WEEK_LABEL` = "DD Month" (e.g., "27 July") — no ordinal suffix
   - `NEXT_UPDATE` = Monday + 7 days, with ordinal suffix + lowercase month (e.g., "3rd august") — matches Vishvesh's style
5. Announce: "Setting up week of {WEEK_LABEL}. Folder created at ~/Personal Work/weekly-updates/YYYY-MM-DD/."

### Phase 2 — Ingest the GitHub Projects screenshot(s)

1. Ask: "Attach the screenshot(s) of this week's rows from GitHub Projects. Multiple screenshots OK — one for shipped last week, one for upcoming, one for explorations."
2. Wait for the screenshot(s).
3. For each row, parse whatever's visible: **Title, Assignees (= PM), Status, Launch Date, Engineering Owner, Design Owner**. Bet/Problem/Description/Outcome are *not* in this view — you'll draft descriptions mechanically from titles and collect richer copy from Vishvesh separately.
4. Classify each row per the framing convention:
   - Launch Date **last week (prior Mon–Fri)** → **Now**
   - Launch Date **this week onwards (next few weeks)** → **Next**
   - Explorations (In Design, Design Ready, Product Scoping, At Risk, etc.) → **Later**
   - Experiments with results → **Signal** (usually separate — Vishvesh dictates these later)
5. If a title is truncated (mid-word ellipsis), ASK for the full text.
6. If a name field is empty (no PM/Design/Eng), leave that segment out of the owner line — do NOT render "TBD" unless Vishvesh explicitly wants a placeholder.
7. Summarize back: "I have N shipped items, M next items, K explorations. Confirm?"
8. **Reality check:** if the screenshot has 5+ shipped items but the Now section only holds 4 (2×2 grid), ASK Vishvesh whether to trim, combine, or handle the extra outside the grid. Do not silently drop items.

### Phase 3 — Intro paragraph decision

Ask: "Include an intro greeting at the top (e.g., 'Hey team, here's this week's update')? Say 'yes', 'skip', or paste your own text."

- If **yes** with no text: draft a 2-paragraph intro (greeting + one-sentence framing). Show it.
- If **skip**: `INTRO_BLOCK` will be an empty string.
- If **user pastes text**: use verbatim.

### Phase 4 — Draft the Now section

Since GitHub Projects doesn't carry the bet/outcome/impact data, default to a lighter draft:

For each **Now** item, draft:
- **Title** — clean version. Prefer the ticket title unless it's clearly a jargony ticket name; then ask Vishvesh what to display.
- **Why sentence** (12-25 words) — mechanical draft from the title. Describe what shipped in plain terms. Do NOT invent outcomes or metrics.
- **Impact pill** — **omitted by default**. The section header ("What we shipped") makes a "Shipped" pill redundant. Only include a pill if Vishvesh dictates a specific outcome (e.g. "New revenue stream", "2 hrs / week saved").
- **Pill color** (if used): coral=revenue, teal=UX/utility, amber=growth, gray=ops/internal.
- **Delay note (optional)** — if Vishvesh mentions a delay, add `<p class="ship-note">1-week delay — REASON</p>` below the card content.

Show ALL draft copy in one block. Wait for edits — expect Vishvesh to iterate on titles/wording and possibly reorder cards.

**Grid balance heuristic:** with the 2×2 grid, cards align by row height. Long-text cards paired with short-text cards leave awkward whitespace. Suggest reordering so both long cards are in one row and both short cards in the other row.

**Odd card count:** `.ship-grid` is flexbox with `flex:0 0 calc(50% - 5px)`. With an odd number of shipped items the last card sits alone on its row at half width, leaving a dead gap. Give that card `style="flex:0 0 100%;"` so its copy expands across the row. Derive this from the count rather than hardcoding a card number, so a 3- or 5-item week both work. Email equivalent: render that card's cell at `max-width:656px` instead of 325px.

### Phase 5 — Draft the Next section

For each **Next** item, draft:
- **Title** — clean from the ticket title.
- **Why sentence** (12-25 words) — mechanical from title unless Vishvesh dictates.
- **Owner line** — combine PM + Design + Eng owners from the GitHub Projects columns. Format: `<b>PM</b> Name · <b>Design</b> Name · <b>Eng</b> Name(s)`.
  - **Omit missing segments entirely** — if there's no Design, render `<b>PM</b> Name · <b>Eng</b> Name`. If there's no Eng, render `<b>PM</b> Name · <b>Design</b> Name`. If both are missing, just `<b>PM</b> Name`.
  - Do NOT use "TBD" as a placeholder unless Vishvesh explicitly asks for one. TBD reads as unfinished; omission reads as "not needed for this item".
- Group by Launch Date. Format the date badge as "DD Month" (e.g., "10 August").
- **Undated items:** if a Next item has no launch date, park in a "Date TBD" group at the bottom OR ask Vishvesh whether to move it to Later.

Show the draft. Wait for edits — owners often come in later batches as Vishvesh confirms with team leads.

### Phase 6 — Handle images

**Feature row with one image (or none):** `.feat-row` is a 2-column grid. One image beside an empty `.feat-img` renders as a large blank beige box that reads as a broken image, not as a placeholder. With exactly one feature image, emit a single slot and set `style="grid-template-columns:1fr;"` on the row. With none, set `{{FEAT_ROW}}` to an empty string and let the shipped grid carry the section. In the email version cap a lone feature image at `max-width:325px`; full width it stretches to ~670px tall and adds a screen of scrolling for one screenshot.

**Feature images dominate file size.** A single un-downscaled feature screenshot took one week's HTML from 94KB to 398KB. If the user drops the feature row, re-check the output size; it should fall back near 100KB.

1. Expected files in `~/Personal Work/weekly-updates/YYYY-MM-DD/images/`:
   - `feature-01.png`, `feature-02.png` — for Now section
   - `next-01.png` ... `next-NN.png` — one per Next item, in display order
   - `proof-01.png` ... `proof-NN.png` — one per experiment (optional)
2. Check what's present: `ls ~/Personal\ Work/weekly-updates/YYYY-MM-DD/images/`.
3. For each missing file, ask: "Missing [filename] for [item]. Drop it in [folder] and reply 'done' — or reply 'skip' to render a gray placeholder."
4. Recheck after each response.
5. For each image found:
   - Copy with `find -exec cp` (handles spaces in filenames).
   - Optimize with `sips`:
     - Feature images: JPEG q=85, max 1400px wide
     - Thumbnails: JPEG q=85, max 300px wide
     - Proof images: JPEG q=85, max 500px wide
   - Base64-encode into a `data:image/jpeg;base64,...` URI.
6. **Passport image special case**: if `feature-02.png` is a passport-photos flow (aspect near 1.17:1) and feature-01 is a wide 3-frame flow (aspect near 1.83:1), pre-crop passport to 1.83:1 with `sips --cropToHeightWidth` so both feature images render at the same size. Ask user before cropping if uncertain.

### Phase 7 — Signal section (experiments)

Ask, in a single prompt:

> "For the Signal section, any experiments with updates this week? For each, provide:
> - **Name**
> - **Hypothesis**
> - **Results** (data, blockers, or 'no signal yet')
> - **Next action**
> - **Verdict**: `running` (blue, still monitoring) / `keep` (green, positive results) / `rollback` (red, reverting) / `defer` (red, pausing) / `iterate` (amber, needs changes)
> - **Proof image** — filename in the images folder, or 'none'
>
> Say 'none' if no experiment updates."

If **none**: `SIGNAL_SECTION` = empty string. Skip the whole section from output.

If **one or more**: draft each experiment card using the pattern below. Show draft. Wait for edits.

### Phase 8 — Later section (explorations)

Data source: same GitHub Projects screenshot, but the exploration items (Design Ready / In Design / Product Scoping / At Risk rows).

For each **Later** item:
- **Stage badge** (from Status column) — normalize the label: "**Product Scoping**" (not "Scoping"), "**In Design**", "**Design Ready**", "**At Risk**".
- **Title** — from ticket.
- **Description** — omit by default (mechanical drafts from codenames like "Offer Island", "BBP" don't help stakeholders). Instead, ask Vishvesh: "Any descriptions you want to add for these? Otherwise I ship title-only." Then add descriptions incrementally as he sends them.
- **Owner meta line** — `<b>PM</b> Name` alone, or `<b>PM</b> Name · <b>Design</b> Name` if Design Owner column has a value. Add target date as `· Target DD Mon` at the end if the date column has a value, **except for Design Ready items — those never show a target date.** Design being ready is a past event, so a date there answers no question a reader has. Use "Target" (neutral) rather than "Launch"/"Handoff" — the GitHub Projects date column doesn't carry unambiguous semantics for exploration items.

**"Ready to Design" is not "Design Ready."** GitHub Projects carries both, in different colours, meaning opposite ends of the design stage. Keep them distinct; never normalize one into the other.

**Sort order (always):**
1. At risk (topmost)
2. Design ready
3. In design
4. Ready to design
5. Product scoping / Discovery / On hold

**Volume check:** 12+ explorations makes the Later section dominate the update. Ask Vishvesh whether to filter (e.g. only bets with movement this week) or ship all.

**Lifting descriptions from prior weeks:** Vishvesh often sends screenshots of an earlier week's rendered exploration cards and asks you to reuse the subtitles. Match on title, and report the match count plainly ("9 of 18 matched"). Titles drift between weeks — "Robot delivery revamp phase 1" is not obviously "Robot delivery - Homepage Onsite Assets" — so surface near-misses and ask instead of assuming. Watch for items that were explorations in a prior week but are shipped or Next this week; their old description is often better than a mechanical draft, but it belongs to a different section, so offer it rather than silently moving it.

**Same as last week shortcut:** if Vishvesh says "same as last week", read `~/Personal Work/weekly-updates/PREV_YYYY-MM-DD/update.html`, extract the explorations block. But **flag stale dates** — last week's target dates are usually past by now.

Draft cards. Show. Iterate as descriptions come in.

### Phase 9 — Generate and preview

1. Read `~/.claude/skills/weekly-update/template.html`.
2. Substitute all tokens:
   - `{{WEEK_LABEL}}` — 2 occurrences (hero + section 01 heading)
   - `{{INTRO_BLOCK}}` — full intro `<div class="intro">...</div>` or empty
   - `{{SHIPPED_COUNT}}` — number of shipped items
   - `{{FEAT_ROW}}` — HTML for feature images row (see fragment)
   - `{{SHIPPED_GRID}}` — HTML for 2×2 shipped-card grid
   - `{{NEXT_COUNT}}` — number of next items
   - `{{NEXT_GROUPS}}` — HTML for date-grouped next items
   - `{{SIGNAL_SECTION}}` — full `<div class="sec signal">...</div>` or empty
   - **Renumber Later when Signal is absent.** The template hardcodes `04 · Later` because Signal is normally 03. With no experiments the reader sees 01, 02, 04 and looks for a missing section. When `{{SIGNAL_SECTION}}` is empty, rewrite the Later chapter to `03 · Later`; when Signal is present, leave it at 04. Do the same in the email version.
   - `{{EXPL_COUNT}}` — number of exploration bets
   - `{{EXPLORATIONS_GRID}}` — HTML for exploration cards
   - `{{NEXT_UPDATE}}` — next Monday's date (e.g., "3rd august")
3. Write output to `~/Personal Work/weekly-updates/YYYY-MM-DD/update.html`.
4. Build the email-safe version. Reference `template-email.html`. Same content, different HTML patterns (table-based, inline-styled). Save to `update-email.html`.
5. Generate PDF from design master (see helper snippet).
6. Generate full-page PNG screenshot from design master (see helper snippet).
7. Open the PDF locally.
8. **Prepare artifact copies first.** Do not publish `update.html` / `update-email.html` directly — they are complete HTML documents, and the Artifact tool wraps the file in its own `<!doctype html><head></head><body>` skeleton. Write stripped copies to the scratchpad that keep `<title>` and `<style>` and the body's inner content, with `<!DOCTYPE>`, `<html>`, `<head>` and `<body>` removed. For the email version, its `<body style="...">` carries the page background, so move those inline styles onto a wrapping `<div>` or the artifact loses its background.

   The artifact CSP blocks external hosts, so the Google Fonts and Tabler CDN `<link>`s never load. Strip them to avoid dead requests. Inter degrades to the system fallback in the artifact only; the local PDF and PNG still render with Inter, so do not "fix" this by editing the template. Verify a stripped copy has zero `https?://` matches before publishing.

9. Publish both HTML files as artifacts (fresh URLs each week — do NOT pass a `url` param):
   - Design master → favicon 📬
   - Email version → favicon ✉️
10. Report to user:
   - Design master URL
   - Email version URL
   - PDF path
   - Screenshot path

### Phase 10 — Confirm and finalize

Ask: "Ready to send? Or any edits?"

- If **send**: done. Optionally, if the user wants, help them with the delivery path (inline screenshot, PDF attachment, or paste email HTML into Gmail).
- If **edits**: iterate on the specific parts. Republish artifacts at the SAME URLs (this time pass `url=[existing artifact URL]` to keep them stable).

## HTML fragment templates

Use these exact patterns. Only replace ALL-CAPS tokens.

### Intro block (used inside `{{INTRO_BLOCK}}`)

```html
<div class="intro">
  <p class="intro-t">GREETING_LINE</p>
  <p class="intro-t" style="margin-top:10px;">CONTEXT_LINE</p>
</div>
```

### Feature image slot (2 needed for `{{FEAT_ROW}}`)

```html
<div class="feat-row">
  <div class="feat-img coral"><img src="data:image/jpeg;base64,BASE64" alt="ALT"></div>
  <div class="feat-img teal"><img src="data:image/jpeg;base64,BASE64" alt="ALT"></div>
</div>
```

### Shipped card (for `{{SHIPPED_GRID}}` — up to 4 cards in `<div class="ship-grid">`)

**Default (no pill — the section header already says "What we shipped"):**
```html
<div class="ship-card">
  <div class="ship-top"><span class="ship-num">NN</span><p class="ship-h">TITLE</p></div>
  <p class="ship-why">WHY_SENTENCE</p>
</div>
```

**With impact pill (only when Vishvesh gives a real outcome):**
```html
<div class="ship-card">
  <div class="ship-top"><span class="ship-num">NN</span><p class="ship-h">TITLE</p></div>
  <p class="ship-why">WHY_SENTENCE</p>
  <span class="ship-pill COLOR"><i class="ti ICON"></i>PILL_TEXT</span>
</div>
```

Optional delay note:
```html
<p class="ship-note">1-week delay - REASON</p>
```

COLOR = coral / teal / amber / gray. NN = 01, 02, 03, 04.

### Next item card

```html
<div class="tl-card">
  <div class="tl-icon"><img src="data:image/jpeg;base64,BASE64" alt="ALT"></div>
  <div>
    <p class="tl-h">TITLE</p>
    <p class="tl-why">WHY_SENTENCE</p>
    <p class="tl-owners"><b>PM</b> NAME · <b>Design</b> NAME · <b>Eng</b> NAME(s)</p>
  </div>
</div>
```

**Owner-line variants — omit missing segments (do NOT render "TBD"):**
- Full team: `<b>PM</b> Name · <b>Design</b> Name · <b>Eng</b> Name(s)`
- No design: `<b>PM</b> Name · <b>Eng</b> Name(s)`
- No engineering: `<b>PM</b> Name · <b>Design</b> Name`
- PM only (early stage): `<b>PM</b> Name`
- Dual PMs (co-ownership): `<b>PM</b> Name1, Name2 · …`

Empty `<div class="tl-icon"></div>` renders as a clean gray placeholder rectangle.

### Next date group (wraps N cards with same launch date)

```html
<div class="tl-group">
  <div class="tl-date">
    <span class="tl-date-badge">DD Month</span>
    <span class="tl-date-line"></span>
    <span class="tl-date-count">N launches</span>
  </div>
  ...tl-cards for this date...
</div>
```

### Signal section wrapper (only if experiments exist)

```html
<div class="sec signal">
  <div class="chapter">
    <span class="chapter-num signal">03 · Signal</span>
    <h2 class="chapter-h">Experiment results and next actions</h2>
  </div>
  ...experiment cards...
</div>
```

### Experiment card (with proof image)

```html
<div class="exp-card">
  <div class="exp-main">
    <div class="exp-header">
      <p class="exp-h">TITLE</p>
      <span class="verdict VERDICT_CLASS"><i class="ti VERDICT_ICON"></i>VERDICT_LABEL</span>
    </div>
    <div class="exp-section">
      <p class="exp-lbl">Hypothesis</p>
      <p class="exp-txt">HYPOTHESIS</p>
    </div>
    <div class="exp-section">
      <p class="exp-lbl">Results</p>
      <p class="exp-txt">RESULTS</p>
    </div>
    <div class="exp-section">
      <p class="exp-lbl">Next action</p>
      <p class="exp-txt">NEXT_ACTION</p>
    </div>
  </div>
  <div class="exp-proof"><img src="data:image/jpeg;base64,BASE64" alt="Proof"></div>
</div>
```

### Experiment card (WITHOUT proof image — full width)

Omit the `<div class="exp-proof">` block entirely. `.exp-main` will take full width.

### Verdict mapping

| Verdict | Class | Icon | Label |
|---------|-------|------|-------|
| Running (blue) | `running` | ti-loader | Running |
| Keep (green) | `keep` | ti-check | Keep |
| Iterate (amber) | `iterate` | ti-refresh | Iterate |
| Rollback (red) | `rollback` | ti-arrow-back-up | Rollback |
| Defer (red) | `kill` | ti-alert-circle | Defer |
| Kill (red) | `kill` | ti-x | Kill |

### Exploration card

```html
<div class="expl-card">
  <p class="expl-stage">STAGE</p>
  <p class="expl-h">TITLE</p>
  <p class="expl-body">DESCRIPTION</p>
  <p class="expl-timeline"><b>PM</b> NAME · <b>Design</b> NAME · Target DD Mon</p>
</div>
```

**Owner + timeline variants — omit segments that don't apply:**
- PM only: `<b>PM</b> Name`
- PM + designer (In Design / Design Ready): `<b>PM</b> Name · <b>Design</b> Name`
- PM + target: `<b>PM</b> Name · Target DD Mon`
- PM + designer + target: `<b>PM</b> Name · <b>Design</b> Name · Target DD Mon`

**Description is optional** — omit `<p class="expl-body">` entirely if Vishvesh hasn't given one.

Stage values (normalized): "At Risk", "Design Ready", "In Design", "Ready to Design", "Product Scoping", "Discovery", "On Hold".

**Do NOT use the `.dark` variant** — all cards equal weight.

## Helper snippets

### Create the week folder
```bash
mkdir -p ~/Personal\ Work/weekly-updates/YYYY-MM-DD/images
```

### Copy image with space-safe filename
```bash
find ~/Personal\ Work/weekly-updates/YYYY-MM-DD/images -maxdepth 1 -name "feature-01.png" -exec cp {} /tmp/f1.png \;
```

### Optimize image
```bash
# Feature image
sips -s format jpeg -s formatOptions 85 -Z 1400 /tmp/f1.png --out /tmp/f1.jpg >/dev/null
# Thumbnail
sips -s format jpeg -s formatOptions 85 -Z 300 /tmp/n1.png --out /tmp/n1.jpg >/dev/null
# Proof image
sips -s format jpeg -s formatOptions 85 -Z 500 /tmp/p1.png --out /tmp/p1.jpg >/dev/null
```

### Pre-crop passport image (special case for near-square images in feature slot)
```bash
# Crop to 1.83:1 aspect (matches wide 3-frame flow)
# Input dims: WxH, target height = W / 1.83
sips --cropToHeightWidth $((W * 100 / 183)) W /tmp/passport-src.png --out /tmp/passport-cropped.png
sips -s format jpeg -s formatOptions 85 -Z 1400 /tmp/passport-cropped.png --out /tmp/passport-fit.jpg
```

### Base64 encode (Python)
```python
import base64
with open("/tmp/f1.jpg", "rb") as f:
    uri = f"data:image/jpeg;base64,{base64.b64encode(f.read()).decode()}"
```

### Render PDF from HTML
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --headless=new --disable-gpu --no-pdf-header-footer \
  --run-all-compositor-stages-before-draw --virtual-time-budget=10000 \
  --print-to-pdf="/Users/vpandya/Personal Work/weekly-updates/YYYY-MM-DD/update.pdf" \
  "file:///Users/vpandya/Personal Work/weekly-updates/YYYY-MM-DD/update.html"
```

### Render full-page PNG screenshot
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --headless=new --disable-gpu --hide-scrollbars \
  --force-device-scale-factor=2 --window-size=760,3400 --virtual-time-budget=10000 \
  --screenshot="/Users/vpandya/Personal Work/weekly-updates/YYYY-MM-DD/update-image.png" \
  "file:///Users/vpandya/Personal Work/weekly-updates/YYYY-MM-DD/update.html"
```

Adjust `--window-size` height if page is longer than 3400px.

### Open PDF for review
```bash
open "/Users/vpandya/Personal Work/weekly-updates/YYYY-MM-DD/update.pdf"
```

## Email-version gotchas

The design master is flex-based; the email version is table-based. Removing content behaves differently in each, and these bite silently.

- **Imageless Next card:** in the master, dropping the `.tl-icon` div collapses the flex gap and the copy aligns to the card edge. In the email the image lives inside `<td width="72">`, so removing only the `<img>` leaves an empty 72px cell and the copy stays indented while the master looks correct. Drop the whole `<td>`, and set the content cell's left padding to 14px so it matches the card edge. Verify by measuring rendered text left-edges, not by eye — imageless cards should cluster around 70px and image cards around 140px at 760px wide.
- **Verdict icons:** the Tabler webfont (`<i class="ti ti-check">`) is an external stylesheet and fails in both artifacts and most mail clients. Use an inline SVG instead, as the prior weeks' files do:
  `<svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" style="flex-shrink:0"><path d="M5 12l5 5L20 7"/></svg>`
- **`.exp-metric` no longer exists** in `template.html`, though older generated weeks reference it. Emphasise a metric with an inline-styled `<b>` or leave it plain. Reserve emphasis for genuine movement; styling a "slight" change in green oversells it.

## Measuring page height

Do not guess `--window-size`. Render tall (`760x9000`), then find the last non-background row with PIL and crop to it:

```python
from PIL import Image
im = Image.open("raw.png").convert("RGB"); W,H = im.size; px = im.load()
bg = px[W-3, H-3]
for y in range(H-1, -1, -1):
    if any(sum(abs(a-b) for a,b in zip(px[x,y], bg)) > 12 for x in range(0, W, 7)):
        last = y; break
im.crop((0, 0, W, last+80)).save("update-image.png")
```

## Failure modes

- **Screenshot too small to read a column:** Ask user to zoom in and re-attach that row's screenshot, or type the missing field.
- **No shipped items this week:** Skip Now section entirely (delete `<div class="sec now">` block). Announce.
- **No next items:** Skip Next section similarly.
- **No experiments:** Set `SIGNAL_SECTION` to empty string. Section disappears.
- **User skips all images:** Render template with empty `.feat-img` / `.tl-icon` / `.exp-proof` blocks — they render as clean gray rectangles.
- **User asks for a design change** (e.g., "make the pills bigger"): Say: "That's a design change, not weekly content. Want to edit the template so future weeks inherit it? That's a separate task." Do not silently modify.
- **User says "same as last week" for experiments or explorations**: Read `~/Personal Work/weekly-updates/PREV_YYYY-MM-DD/update.html`, extract the relevant section, reuse.
- **Uploaded chat images that never landed on disk**: Chat-attached images don't get saved to disk automatically. Ask user to right-click → Save Image As, then tell you the file path. Explain that the "attach in chat" gesture only lets you *see* the image, not extract it as a file.

## What NOT to do

- Do not fabricate any data — names, dates, metrics, statuses. If unclear, ASK.
- Do not use em dashes (—) anywhere. Use hyphens, commas, or rewrite.
- Do not make one card visually heavier than others (no `.dark` variant, no flagship treatment).
- Do not use these words: delve, leverage, furthermore, moreover, additionally, ultimately, seamlessly, robust, comprehensive, cutting-edge, unlock, empower.
- Do not publish an artifact before showing preview and getting confirmation.
- Do not overwrite previous week's folder or artifact URLs.

## First-run behavior

If `~/Personal Work/weekly-updates/` doesn't exist:
1. `mkdir -p ~/Personal\ Work/weekly-updates/`
2. Announce: "First run detected. Creating the weekly-updates archive folder."
3. Proceed with Phase 1.

## Reference — current canonical example

The finalized example from the 17 July edition lives at:
- Design master: `~/Personal Work/weekly-product-update.html`
- Email version: `~/Personal Work/weekly-update-email.html`

Use these as the visual reference. When in doubt about card structure, spacing, colors, or copy voice — open one of these and mirror it.
