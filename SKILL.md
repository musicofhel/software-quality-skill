---
name: software-quality
description: Run a software quality audit — six signals (reliability, speed, clarity, efficacy, efficiency, beauty), seven adversarial execution passes, measurable thresholds, code-level smell greps, and a papercut checklist. Use for quality audits, polish passes, papercut hunts, UX reviews, pre-launch checks, or when asked to make software feel higher quality.
---

# Software Quality Audit

Framework spine from Anthony Hobday's ["Notes on software quality"](https://anthonyhobday.com/blog/20260410);
operational detail extends it.

## Core premise

**Quality is the absence of problems.** You cannot add quality directly — you find
problems and remove them. So an audit is a structured, adversarial problem hunt.
Two consequences shape how you run it:

- **You must try to break things.** The happy path proves nothing; every signal
  below has a sabotage angle. If you finish an audit with zero findings, you
  didn't audit — you demoed.
- **Diminishing returns are real.** Going from 80% to 90% costs more than getting
  to 80% did. The report must rank findings so effort lands where users feel it,
  not where problems were easiest to find.

## Process

1. **Scope.** Diff, feature, screen, flow, or whole app. Identify the **top 3 user
   tasks** in scope — most of the audit orbits these. If the software runs, run it;
   half the passes below only work live.
2. **Static sweep.** Read the code with the smell greps below before touching the UI.
3. **Execution passes.** Run the seven passes below against the live software.
4. **Signal review.** File every finding under one of the six signals, severity-rated.
5. **Papercut checklist.** For UI scope, walk [checklist.md](checklist.md) item by item.
6. **Report.** Format below. Audit only — don't fix unless asked.

## Static sweep — code smells that predict user-facing problems

Grep before you click. Each of these correlates with findings you'll confirm live:

- **Swallowed errors**: bare `except:`/`except Exception: pass`, empty `catch {}`,
  `.unwrap()`/`!` force-unwraps, ignored error returns, `catch (e) { console.log(e) }`
  with no user feedback. Every one is a future silent failure (Reliability + Clarity).
- **N+1 and waterfalls**: queries inside loops, sequential `await`s that could be
  `Promise.all`, ORM lazy-loads in list renders (Speed).
- **Missing states**: components with no loading/empty/error branch — search for
  data-fetching code and check all three exist (Clarity).
- **Unbounded work**: queries without `LIMIT`, lists without pagination or
  virtualization, file reads without size checks (Speed + Reliability).
- **Race invitations**: submit handlers that don't disable/guard against
  double-fire, non-idempotent POSTs, missing optimistic-lock/version checks
  (Reliability).
- **Hardcoded assumptions**: locale (`,` vs `.` decimals), timezone
  (`new Date()` math without TZ), fixed pixel widths around user text, English
  string-length assumptions (Reliability + Beauty).
- **Inconsistent vocabulary**: the same concept under different names across code,
  UI strings, and docs — it will leak into the interface (Clarity).

## Execution passes

Run these against the live software, in this order. Each pass has a target signal
but files findings anywhere.

1. **First-run pass.** Fresh state, no data, no cookies. Is the empty state
   designed (explains + offers the primary action) or accidental (blank table,
   `null`, spinner forever)? Is onboarding survivable without a tour?
2. **Happy-path pass.** Do the top 3 tasks end to end. **Count clicks and
   keystrokes** for each — the count is data for the Efficiency review. Note any
   moment you hesitated: hesitation is a Clarity finding even if you recovered.
3. **Keyboard-only pass.** Unplug the mouse mentally. Tab order sane? Focus always
   visible? Enter submits, Escape dismisses? Can every interactive element be
   reached and operated? Modals trap focus and return it on close?
4. **Sabotage pass.** Throttle to slow 3G. Go offline mid-action. Double-click
   every submit. Refresh mid-form. Use the back button mid-flow. Paste a
   200-character name, an emoji, `"><script>`, a decimal comma, a RTL string.
   Upload the wrong file type and a 500MB file. Open the same record in two tabs
   and edit both. Let a session expire, then act.
5. **Error-path pass.** Trigger every error you can and *read the messages*. Each
   must say what happened, why (if known), and what to do next — in the user's
   vocabulary, without blame, without codes-as-messages (`Error: E_FETCH_FAILED`
   is a finding).
6. **Resize & stress pass.** Narrow window, 200% browser zoom, OS font scaling,
   very long user-generated strings in every label slot, 10,000-row list.
   Truncation with no tooltip, overlap, layout collapse — all findings.
7. **Squint pass.** Zoom out / screenshot and blur. Does hierarchy survive — do
   the important things read as important? Then at 100%: spacing consistent to a
   scale, alignment to a grid, icon stroke weights uniform, one thing visually
   "off" per screen max.

## The six signals

Review findings under these, and use each signal's bar to hunt for what the passes missed.

### 1. Reliability — works, all of the time
The bar: no action loses user data; no state is unrecoverable; concurrent and
repeated actions are safe (idempotent or guarded); interruption (kill, refresh,
offline) leaves the system consistent. Edge-case taxonomy worth walking: empty,
one, many, huge; unicode; timezone/DST boundaries; leap days; clock skew; expired
auth mid-flow; permissions changing under you.

### 2. Speed — responds instantly, or as near as practical
Thresholds (from HCI research — RAIL and Nielsen's response-time limits):
**<100ms** feels instant (button feedback, typing echo, menu open); **<1s** keeps
flow (page transitions, search results); **>1s needs a progress indicator**;
**>10s needs a cancel button and a time estimate**. Perceived speed counts:
optimistic updates, prefetch on hover, skeleton screens over spinners,
stale-while-revalidate. A fast backend behind a janky main thread is still slow.

### 3. Clarity — the user understands everything
The bar: labels use the user's vocabulary, not the schema's; one concept has
exactly one name everywhere; every icon-only control has a label or tooltip;
every state the system can be in is visible and explained (loading, empty, error,
partial, stale); dates show relative *and* absolute; nothing fails silently.
Test: could a new user narrate what each screen element does? Every "probably..."
is a finding.

### 4. Efficacy — the user can actually do the thing
The bar: the top 3 tasks complete without leaving the product, without
workarounds, without asking anyone. Hunt for dead ends (states with no forward
action), trapped data (no export/import/undo/recover), and the workaround smell —
if users would keep a spreadsheet on the side, the product is failing at
something it should do.

### 5. Efficiency — as easily as possible
The bar, using the counts from pass 2: frequent tasks in the fewest possible
steps; defaults match what most users pick (a default everyone changes is a
finding); the software remembers context (last-used folder, previous choices,
draft state); bulk operations exist wherever users repeat an action; power users
get shortcuts without novices needing them; first field autofocused; tab order
matches visual order.

### 6. Beauty — as aesthetically pleasing as possible
The bar: spacing from a consistent scale (4/8px or equivalent) — measure, don't
vibe; a deliberate type scale, not ad-hoc sizes; optical alignment where geometry
lies (icons next to text, triangles in circles); a bounded palette used
consistently; motion sharing duration/easing tokens; dark mode (if offered) at
full parity, not an afterthought. "Looks off but I can't say why" is not a
finding — figure out why; that's the finding.

## Severity rubric

- **Blocker** — data loss, unrecoverable state, core task impossible, security hole.
- **High** — users hit it in the top 3 tasks; workaround exists but hurts.
- **Medium** — noticeable on secondary paths, or a top-task annoyance with an
  easy workaround.
- **Papercut** — individually trivial; collectively the difference between
  software that feels crafted and software that feels extruded. Report them all —
  papercuts are the audit's main cargo, and "if something is low quality, it's
  usually a reliable sign other things are" cuts both ways.

## Report format

1. **Verdict** — one honest paragraph: overall level, the dominant problem theme,
   and which signal is weakest. Organisations almost never tell the truth about
   the low quality of their products; an audit that flatters is worthless.
2. **Findings table** — signal · location (`file:line` or screen/element) ·
   description · severity.
3. **Papercut list** — checklist misses plus pass findings, flat list.
4. **Top 3 fixes** — where effort buys the most felt quality. Prefer one fix that
   removes a class of problems (e.g. "add the missing error/empty/loading states
   everywhere") over three one-offs.

## Attribution

The six signals, quality-as-absence-of-problems, and the seed of the papercut
checklist are Anthony Hobday's —
[anthonyhobday.com/blog/20260410](https://anthonyhobday.com/blog/20260410). The
essay is worth reading in full for what a skill can't hold: why quality gets
harder with scale, and how Linear, Zed, GitLab, Automattic, and Stripe structure
dedicated quality efforts.
