# software-quality — a Claude Code skill

A [Claude Code](https://claude.com/claude-code) skill that audits software against
the **six signals of software quality** — reliability, speed, clarity, efficacy,
efficiency, beauty — plus a 20-point interface quality-of-life checklist.

Distilled (paraphrased, with full attribution) from Anthony Hobday's essay [**Notes on software quality**](https://anthonyhobday.com/blog/20260410).
The core idea: *quality is the absence of problems*, so an audit is a structured
problem hunt — sweep each signal, record every problem, rank by user impact.

## Install

```bash
git clone https://github.com/musicofhel/software-quality-skill ~/.claude/skills/software-quality
```

Restart Claude Code (or start a new session) and the skill is available.

## Use

Ask Claude Code things like:

- "Run a software-quality audit on this PR"
- "Do a polish pass on the settings screen"
- "Hunt for papercuts in the dashboard"

Or invoke it directly: `/software-quality`

The skill produces a report — verdict, findings table by signal and severity,
papercut list from the interface checklist, and the top 3 fixes where effort buys
the most quality. It audits; it doesn't change code unless you ask it to fix the
findings.

## Contents

- [`SKILL.md`](SKILL.md) — the skill: core premise, audit process, the six signals
  with problem types to hunt for, and the report format.
- [`checklist.md`](checklist.md) — the interface quality-of-life checklist,
  grouped into pointer/keyboard forgiveness, motion, spatial stability, and
  data/feedback.

## Attribution

The framework is Anthony Hobday's, paraphrased from
[anthonyhobday.com/blog/20260410](https://anthonyhobday.com/blog/20260410).
Read the full essay — it goes much further: why quality gets harder with scale
(with a great collection of industry testimony), and how companies like Linear,
Zed, GitLab, Automattic, and Stripe structure dedicated quality efforts.

## License

MIT (covers the skill packaging in this repo; the underlying ideas belong to their
author, credited above).
