# software-quality — a Claude Code skill

A [Claude Code](https://claude.com/claude-code) skill that runs an adversarial
software quality audit. The framework's spine is Anthony Hobday's
[**Notes on software quality**](https://anthonyhobday.com/blog/20260410) — quality
is the absence of problems, judged through six signals — fleshed out into an
operational playbook an agent can actually execute.

## What's in the audit

- **Static sweep** — code-smell greps that predict user-facing problems before the
  app is even launched: swallowed errors, N+1 queries, missing loading/empty/error
  states, unguarded double-submits, locale/timezone assumptions.
- **Seven execution passes** — first-run, happy-path (with click/keystroke
  counting), keyboard-only, sabotage (throttling, offline, double-clicks, hostile
  input, two-tab edits), error-path, resize & stress, and the squint pass.
- **The six signals** — reliability, speed, clarity, efficacy, efficiency, beauty —
  each with a concrete bar and measurable thresholds (100ms/1s/10s response-time
  limits, spacing scales, error-message anatomy).
- **Papercut checklist** ([`checklist.md`](checklist.md)) — ~60 items across
  pointer forgiveness, focus & keyboard, motion, spatial stability, forms,
  feedback, and words. Hobday's original 20 are marked `[H]`; the rest extend them.
- **Severity rubric + report format** — blocker/high/medium/papercut, an honest
  verdict, and a top-3-fixes section that favors class-of-problem fixes over
  one-offs.

## Install

```bash
git clone https://github.com/musicofhel/software-quality-skill ~/.claude/skills/software-quality
```

Restart Claude Code (or start a new session) and the skill is available.

## Use

- "Run a software-quality audit on this PR"
- "Do a polish pass on the settings screen"
- "Hunt for papercuts in the dashboard"
- "Pre-launch quality check on the app"

Or invoke it directly: `/software-quality`

It audits; it doesn't change code unless you ask it to fix the findings.

## Attribution

The six signals, the quality-as-absence-of-problems framing, and the seed of the
papercut checklist are Anthony Hobday's, from
[anthonyhobday.com/blog/20260410](https://anthonyhobday.com/blog/20260410).
Read the full essay — it covers what a skill can't: why quality gets harder with
scale (with a great collection of industry testimony), and how companies like
Linear, Zed, GitLab, Automattic, and Stripe structure dedicated quality efforts.
The extensions here draw on standard HCI research (Nielsen's response-time
limits, RAIL) and general interface craft.

## License

MIT (covers this repo's packaging and extensions; the original framework belongs
to its author, credited above).
