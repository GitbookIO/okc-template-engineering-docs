---
title: Update systems
description: Keep each System page current from its pull requests, issues, incidents and specs, and flag where code drifts from approved specs.
icon: server
on: '{prs,issues,incidents,specs}/**'
commit: branch
files:
  '**': read-only
  systems: read-write
  log.md: read-write
---

You keep the System pages in `systems/` current. Each page says what a system does, who owns it, what changed, what's open, and where shipped code disagrees with its approved specs.

## Which pages to update

Read the records that triggered this run. Collect every System page they link to in `system` or `systems`. Update only those pages.

If a record links to a system that has no page yet, create `systems/<slug>.md` for it, using the slug from the link, with `status: draft`. Fill it from the records that link to it, like any other page: `title` from the slug or the repository's name, `description` in one line from what the records show, `team` if its issues agree on one, `repository` from its pull requests, and `depends_on: []`. Leave out `lifecycle`. People remove `status: draft` once they've reviewed the page, so never add it to an existing page or remove it yourself.

## What to read for each system

- The current page, `systems/<slug>.md`. Keep what people wrote there unless the records contradict it.
- Every record that links to it: search `prs/`, `issues/`, `incidents/` and `specs/` for `/systems/<slug>.md` in frontmatter.
- Decisions in `decisions/` and runbooks in `runbooks/` that link to it.

## What to write

Frontmatter:

- Keep `type`, `title`, `description`, `team`, `lifecycle`, `depends_on` and `repository`. Change them only when a record says so explicitly.
- `specs`: every Spec with `state: approved` that lists this system.
- `runbooks`: every Runbook whose `system` is this system.
- `sources`: one entry per record you cite, with `resource` as its bundle path (`/prs/mock-3.md`), `title`, and `id` as `<folder>-<filename without .md>` (`prs-mock-3`).
- `generated`: the workflow signature you were given, with `at` set to now.
- `stale_after`: 30 days after `generated.at`.
- Keep `verified` as it is. It records when a person last confirmed the page.

Body, in this order:

1. One paragraph on what the system does and who relies on it.
2. `## Owner and dependencies`: the owning team, then a Mermaid `flowchart LR` from this system to each system in `depends_on`.
3. `## Recent changes`: merged pull requests from the last 30 days, newest first, one line each with a footnote, like `- Charge retries are idempotent.[^prs-mock-3]`.
4. `## Open issues`: issues whose `state` isn't done or canceled, highest priority first, with footnotes.
5. `## Incidents`: incidents from the last 90 days, newest first, with what happened in one line and a footnote.
6. `## Drift from spec`: for each approved spec in `specs`, compare what it requires with what pull requests merged since its `approved_at` actually did. List each disagreement as one line that says what the spec requires and what shipped, citing both, like `- The spec requires 5 retries. Retries now stop after 3.[^specs-mock-2][^prs-mock-7]`. If a spec has no drift, write `No drift found against <spec title>.` with its footnote. Only list disagreements the text of both records shows. Don't guess.
7. `## Activity`: a Vega-Lite bar chart in a `vega-lite` code block of issues opened per week over the last 6 weeks, counted from the `created_at` of this system's issues.

Use footnotes for every claim that comes from a record. Define no footnotes in the body: the `sources` ids are the footnote labels.

## Index

Keep `systems/index.md` as a list of every System page: `- [<title>](<slug>.md): <description>`, sorted by title.

## Log

Add one line to `log.md` under today's `## YYYY-MM-DD` heading (create it at the top if missing):
`- **Update** <system titles> from <n> records, <n> drift findings, by update-systems.`
