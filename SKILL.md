---
name: software-quality
description: Audit software against the six signals of software quality (reliability, speed, clarity, efficacy, efficiency, beauty) plus a 20-point interface quality-of-life checklist, distilled from Anthony Hobday's "Notes on software quality". Use for quality audits, polish passes, papercut hunts, UX reviews, or when asked to make software feel higher quality.
---

# Software Quality Audit

A framework for finding and fixing quality problems in software, distilled from
Anthony Hobday's essay ["Notes on software quality"](https://anthonyhobday.com/blog/20260410).

## Core premise

**Quality is the absence of problems.** You cannot add quality directly — you find
problems and remove them. The most reliable way to measure quality is to have many
people (and experts) look hard at the thing. So an audit is a structured problem hunt:
sweep the software through each signal below, record every problem found, then rank
by user impact.

Keep two principles in mind while auditing:

- **Diminishing returns.** Going from 80% to 90% quality costs more than getting to
  80% did. Rank findings so effort lands where users feel it most.
- **Quality erodes silently.** Problems slip in as changes are made, especially in
  software that grows. An audit is a point-in-time snapshot — recommend re-running
  it after significant change, not treating it as done forever.

## Process

1. **Scope.** Identify what is being audited: a diff, a feature, a screen, a flow,
   or a whole app. If it's a running interface, actually run it and interact with it
   (use the project's run/verify tooling) — many problems below are only visible live.
2. **Sweep the six signals.** Work through each signal in order. For each, actively
   hunt for problems; don't just confirm the happy path.
3. **Run the interface checklist.** If the scope includes UI, go through
   [checklist.md](checklist.md) item by item and note each miss.
4. **Report.** Output findings as described below. Do not fix anything unless asked —
   the audit is the deliverable.

## The six signals of quality

For each signal, the question to answer and typical problems to hunt for:

### 1. Reliability — does it technically work, all of the time?
Hunt for: bugs, unhandled errors, race conditions, flaky behavior, crashes, data
loss, broken edge cases (empty states, huge inputs, slow networks, concurrent use).

### 2. Speed — does it respond instantly, or as near as practical?
Hunt for: slow initial load, laggy input response, operations that block the UI,
missing progress feedback on unavoidably long tasks, redundant network round-trips,
N+1 queries, unnecessary re-renders.

### 3. Clarity — does the user understand everything?
Hunt for: ambiguous labels, jargon, unexplained states, silent failures, error
messages that don't say what to do next, features whose purpose isn't discoverable,
inconsistent terminology across screens.

### 4. Efficacy — can the user actually do what they need to do?
Hunt for: missing capabilities in the core flow, dead ends, tasks that require
workarounds or leaving the product, features that exist but don't produce the
result the user came for.

### 5. Efficiency — can they do it as easily as possible?
Hunt for: extra clicks/steps in common tasks, missing keyboard shortcuts, forms
that ask for things the software already knows, no bulk operations where users
repeat an action, poor defaults that everyone changes.

### 6. Beauty — is it as aesthetically pleasing as possible?
Hunt for: misaligned or optically unbalanced elements, inconsistent spacing/type/
color, visual clutter, missing or janky motion, elements that look "off" even if
you can't immediately say why (say why — that's the finding).

## Output format

Produce a report with:

1. **Verdict** — one paragraph: overall quality level and the dominant problem theme.
2. **Findings table** — each problem with: signal, location (file:line or screen/
   element), description, and severity (high = users hit it in core flows, medium =
   noticeable but survivable, low = papercut).
3. **Papercut list** — the interface-checklist misses, as a flat list. Individually
   small; collectively they are what makes software feel low quality.
4. **Top 3 fixes** — where effort buys the most quality, per the diminishing-returns
   principle.

Be honest in the verdict. Organisations almost never tell the truth about the low
quality of their products; the audit is only useful if it does.

## Attribution

The six signals, the quality-as-absence-of-problems framing, and the interface
quality-of-life checklist are Anthony Hobday's, from
[anthonyhobday.com/blog/20260410](https://anthonyhobday.com/blog/20260410)
(paraphrased here). Read the full essay — it also covers why quality gets harder
with scale, and how companies like Linear, Zed, GitLab, and Stripe run dedicated
quality efforts.
