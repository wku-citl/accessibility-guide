# Accessibility Starting Points

A self-guided reference tool built by WKU's Center for Innovative Teaching & Learning (CITL) to help faculty review their own course materials for accessibility, organized by the content types they actually use rather than as a single, generic checklist.

---

## What this is

Faculty select the content types in their course (PowerPoint, Word, PDFs, images, video/audio, Blackboard documents, quizzes, links), and the tool filters down to only those — for each one, why a given issue matters, what Blackboard Ally and other built-in checkers can and can't tell you about it, and one clear next step. A lightweight review log lets faculty track what they've addressed as they go and copy that record out for their own future reference.

## What this isn't

- **Not a replacement for the CITL website** or the printable one-page guides. Each section links out to the relevant one for anyone who wants the fuller how-to.
- **Not a compliance determination tool.** It doesn't certify a course as meeting WCAG/ADA requirements, and it deliberately avoids governance questions (thresholds, monitoring, official documentation requirements) that belong to the Office of Institutional Equity, not CITL.
- **Not a substitute for Ally.** It's built to help faculty use Ally's score and report more productively, not to replace or duplicate what Ally already does.

## How it works

1. Faculty check off the content types their course actually uses.
2. The tool shows one content type at a time (as tabs), each with a short list of items to review.
3. Each item expands to show: **why it matters**, **what the checkers tell you** (and don't), and **what to do**.
4. Items are tagged by tier:
   - **Core fix** — squarely the faculty member's own work, and achievable.
   - **Worth a CITL conversation** — bigger lift or genuine judgment call; flagged for a consult, not a five-minute fix.
   - **Not expected of you** — outside what a faculty member can reasonably fix themselves (e.g., something requiring Adobe Acrobat Pro, or a third-party vendor's tool).
5. A running "Accessibility review log" lets faculty check off items as they address them and copy the result out for their own records.

## Content covered

PowerPoint/Slides · Word documents · PDFs & scanned documents · Images & graphics · Video & audio · Blackboard documents · Quizzes & assessments · Links & external resources

## For anyone editing this file

This is a single, self-contained HTML file — no build step, no framework, no dependencies beyond a Google Fonts import. Everything (the content-type picker, tabs, and all item content) is generated from one JavaScript array, `CATEGORIES`, near the top of the `<script>` block.

**Each category has:**
```js
{
  id: "ppt",              // used internally for tab/panel IDs — keep short, no spaces
  label: "PowerPoint / Slides",
  intro: "...",            // one-line description shown at the top of the tab
  goDeeper: "...",         // HTML string with a link out to the website or a PDF guide
  items: [ /* see below */ ]
}
```

**Each item has:**
```js
{
  title: "...",
  tier: "do" | "ask" | "not",         // controls color + which tierLabel applies
  tierLabel: "Core fix" | "Worth a CITL conversation" | "Not expected of you",
  why: "...",                          // why this matters, in plain language
  checks: ["...", "..."],              // what automated checkers can/can't tell you — an array, can be one item or several
  action: "...",                       // the concrete next step
  wku: "..."                           // OPTIONAL — only for WKU-specific tool/vendor notes (renders as a highlighted "At WKU:" box)
}
```

**Item ordering convention:** within each category, list `"do"` items first, then `"ask"`, then `"not"` — so every category opens with something achievable and closes with anything genuinely out of the faculty member's hands.

### ⚠️ The one bug that will break the whole page

Every text field above is a JavaScript string wrapped in **straight double quotes** (`"..."`). If you type a normal quotation mark *inside* one of these fields — e.g., writing `the "Roster" page` — it will end the string early and throw a syntax error that silently breaks the **entire script**, not just that one item. When this happens, the whole content-type picker disappears, because the code that builds it never runs.

If you need a quoted term or phrase inside any field, use the curly-quote escapes already used throughout the file instead of straight quotes:

```js
// Breaks the whole page:
action: "apply it from the "Roster" page."

// Safe — matches the existing style:
action: "apply it from the \u201CRoster\u201D page."
```

Single quotes (`'Roster'`) also work and don't need escaping, if you'd rather use those.

**Before committing any change**, open the file in a browser and confirm the content-type checkboxes still appear and the whole flow (select → continue → tabs → log) still works. A broken picker with no visible error message is almost always this exact issue.

## Known open items

- Content accuracy is being reviewed one category at a time — PowerPoint and PDFs have had close passes; others are still pending.
- The "go deeper" links point to the general CITL accessibility page except where a dedicated printable guide exists (currently PowerPoint and Word); this mapping may need revisiting as new one-pagers are added.
- No screen reader (NVDA) pass has been done yet — accessibility of this tool itself has so far been verified through code-level contrast checks and automated interaction testing, not a live assistive-technology run-through.
- References Ally features (e.g., PDF auto-tagging) that are new as of mid-2026; wording may need adjusting as that feature matures or its interface changes.

## Contact

Built and maintained by WKU CITL. Questions or suggestions: citl@wku.edu.
