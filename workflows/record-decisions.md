---
title: Record decisions
description: Record each decision made in a discussion or spec, with its options, reasons and who decided.
icon: scale-balanced
on: '{discussions,specs}/**'
commit: branch
files:
  '**': read-only
  decisions: read-write
  log.md: read-write
---

You record decisions in `decisions/`, so the reasons behind them outlive the thread or spec they came from.

For each Discussion or Spec record that triggered this run:

1. Read it, and the decisions in `decisions/` that link to the same systems.
2. Find each decision in it. A decision is a choice between options that people agreed on, or a spec reaching `state: approved`. A proposal nobody agreed to yet is a decision with `state: proposed`. Questions and status updates aren't decisions. If there's no decision, write nothing.
3. If a decision page for the same choice exists, update it. Otherwise create `decisions/<YYYY-MM-DD>-<slug>.md`, dated the day it was decided, like `decisions/2026-10-21-queue-webhook-retries.md`.
4. Frontmatter from `types/Decision.md`: `type: Decision`, `title` (the choice, as a statement), `description` (one line), `state`, `decided_on`, `deciders` (the people who agreed, by name, as the record names them), `systems`, `supersedes` (an earlier decision this one replaces, if it does), `sources` (with `resource` as the bundle path and `id` as `<folder>-<filename without .md>`), `generated` (the workflow signature you were given, `at` now) and `stale_after` (180 days later).
5. Body:
   - `## Decision`: what was decided, in one or two sentences.
   - `## Options considered`: a Mermaid `flowchart TD` from the question to each option, with the chosen one styled, then one line per option.
   - `## Reasons`: why this option won, in the deciders' own reasoning, with footnotes.
   - `## Consequences`: what changes because of it, and what it rules out.
   - `## Who decided`: the deciders and the date.

If a new decision replaces an older one, set the older page's `state` to `superseded`.

Keep `decisions/index.md` as a list of every decision, newest first: `- [<title>](<file>.md): <description>`.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Record** <n> decisions from <n> discussions and specs, by record-decisions.`
