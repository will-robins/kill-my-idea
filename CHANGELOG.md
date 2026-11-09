# Changelog

## 0.6.1 — 2026-11-09

- `roast` now points to the right sections of the kill skill. It runs sections 0–5, so the safety rules and the scoring are no longer skipped, and it takes the verdict card from section 6 instead of section 5.

## 0.6.0 — 2026-11-09

**Features**
- **Share card.** A new button in the report downloads a 1200×675 PNG verdict card (score ring, verdict, key finding) for X, LinkedIn or Reddit. It's drawn in your browser; nothing is uploaded.
- **`/kill-my-idea:check-tweet`.** Fact-checks a viral "make money" post: every claim checked, the headline number recomputed from real fees and prices, the author's offer named, and a kill-my-idea verdict on the opportunity.
- **Reports in French.** Labels follow the idea's language (`idea.language`: `en` or `fr`), including country names and dates.

**Hardening**
- Strict Content-Security-Policy, with the only inline script pinned by sha256 (`scripts/update-csp.py`). No network calls except fonts.
- Data validation: malformed `report-data.js` shows a clear error card instead of a blank page. Strings are capped at 4000 characters and lists have limits.
- The skill gets a "Safety and integrity" section: fetched content is never instructions, no invented URLs, no actions, and a 5-point self-check before files are written.
- New `SECURITY.md` with the threat model and the known limitation.
- Reviewed with a security review of the changes (no findings) and tested with 15 injection attempts, a malformed data file, French data, and the share card.

## 0.5.1 — 2026-11-09 (security)

The report shows content gathered from web research, so it must never run code found in that content.
- **Links:** source and competitor links are only rendered for `http(s)` URLs. A `javascript:` or other scheme is shown as plain text.
- **Tooltips:** tooltips are now plain text, inserted with `textContent`. A hostile string in a reasoning note, a competitor name, a risk or a scenario can no longer run code on hover.
- **Data normalization:** fields rendered without escaping (scores, traction, prices, risk levels, verdict, difficulty) are forced to numbers or known values when the data loads.
- Tested with 15 injection attempts. The previous version ran one of them and kept 3 `javascript:` links; this version runs none and keeps no such links. Thanks to the reviewer who reported the link issue.

## 0.5.0 — 2026-11-09

- **New kill shot: saturated wave.** Flags ideas that belong to a flood of near-identical launches in the last 6–12 months (AI wrappers, "100 tools in your browser", Notion template packs…). It counts look-alike launches on Product Hunt, Show HN, r/SideProject, GitHub and X, and names examples. A fixed rule applies: a saturated wave with no specific edge caps Competitive room and differentiation at 1.5. Suggested by u/medialantern on r/ClaudeCode. Thanks!

## 0.4.0 — 2026-11-09

- **Fixed scroll lag.** The section tabs no longer scroll the page, the sticky header has no blur effect, and tooltips update at most once per frame.
- **Answer-first structure.** The report now opens with an executive summary (3 key findings, the KPIs, one recommendation), followed by the rescue paths, the 7-day test, the evidence, market, competition, unit economics, countries, risks, scoring and sources.
- **More granular score.** 21 sub-scores, three per criterion, in half points, each with a one-line justification and a source. Click a criterion to expand it; all sub-scores print in the PDF.
- **Writing standard.** Concise text, highlighted keywords (`**like this**`), professional vocabulary, and named primary sources with their year, e.g. "(INSEE, 2025)".
- New fields: `key_findings`, `recommendation` and `criteria_detail`.

## 0.3.0 — 2026-11-09

The HTML report was rewritten from scratch with the ui-ux-pro-max design system ("Data-Dense Dashboard" for financial analytics).
- Light blue and slate palette with Fira Sans and Fira Code. Dark mode follows the system setting.
- Layout: a sticky top bar with the verdict and a "Save PDF" button, section tabs, a hero card with a score ring, KPI cards, rescue-path cards, chart cards and data tables.
- Verdict colors are reserved for verdicts, with vivid fills and darker text for 4.5:1 contrast.
- Lucide icons, hover and focus states, 44px touch targets, and checked layouts at 375, 768, 1024 and 1440px.
- Motion: the score ring counts up, the verdict badge pops in, cards fade in one after another (400ms), and bars fill when they come into view. Reduced motion, printing and a fallback timer all show the final state.
- The data format (`report-data.js`) is unchanged, so earlier reports still render.

## 0.2.1 — 2026-11-09

The HTML report was reworked after a design critique.
- Removed generic AI patterns: section numbers, monospace labels, the colored left border, metric tiles, text glyphs used as icons, middle dots and boilerplate copy.
- Key figures are now a table that says what each number means ("Each paid customer loses money.").
- Icons are drawn SVG in one stroke weight. Text selection, scrollbar, caret and table numerals are themed.
- One load animation: the score counts up with the gauge, then the verdict stamp presses down with an ink texture. Bars fill once when they scroll into view. Reduced motion, printing and a timer all show the final state.

## 0.2.0 — 2026-11-09

- **HTML report** (`report.html` + `report-data.js`): a consultant-grade dossier in an editorial noir design.
  - Charts: score gauge, scorecard, market funnel, competitor map, LTV:CAC bullet chart, scenario bars, risk matrix.
  - Every number shows whether it is sourced, an estimate or unknown, and sources are numbered footnotes.
  - Sticky table of contents, hover tooltips and keyboard access.
  - Works offline and prints to A4 PDF in a light theme.
- **"Could it be saved?"**: NO-GO and PIVOT verdicts now come with up to 3 rescue paths. Each has a projected score, a difficulty (doable / hard / very hard), effort, cost and requirements. They appear on the card, in the report and in `verdict.json`.
- `compare` shows the best rescue path; `deepdive` refreshes the HTML report with customer quotes and the competitor teardown.
- New `report-data.schema.json`.

## 0.1.0 — 2026-11-09

First release.

- `/kill-my-idea:kill`:
  - idea-brief extraction (`idea.json`) and up to 4 intake questions;
  - an 8-item kill-shot checklist;
  - a metrics block (TAM/SAM/SOM, CAC, LTV, LTV:CAC, payback, break-even, time to first €);
  - a weighted score out of 100 with hard rules;
  - the verdict card, badge, `verdict.json` and a 7-day test with kill criteria.
- `/kill-my-idea:deepdive`: 6 parallel research tracks, 20+ sources, a country comparison and a launch-country recommendation.
- `/kill-my-idea:roast`: 5 sourced burns plus the verdict card.
- `/kill-my-idea:compare`: ranks every `verdict.json` in the project and picks one focus.
- Country-aware research: local competitors, prices in local currency, laws and channels.
- Real example verdicts: coloring book, KDP books, travel affiliate site, Juicero, and the plugin itself.
