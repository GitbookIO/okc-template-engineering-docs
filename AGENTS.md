# Instructions for agents

This repo is Acme's engineering docs: what each system does, who owns it, what changed, what was decided, and how to fix known problems. Workflows keep it current from pull requests, issues, incidents, specs and chat threads, and people review every change. These instructions are for agents connected over MCP or through the desktop app.

## Find your way

1. Read `index.md` first. There is no search, so it's the map: it lists every folder.
2. Open the `index.md` of the folder you need. Each concept folder lists its pages there.

   Concept folders, written by workflows, each with an `index.md`:

   - `systems/`: one page per system, with its owner, dependencies, recent changes, open issues, incidents and drift from spec. Start here for questions about how something works.
   - `teams/`: one page per team and what it owns.
   - `decisions/`: one page per decision, with the options, reasons and who decided.
   - `runbooks/`: how to recognize and fix a known kind of problem.
   - `skills/`: agent skills on how to change each busy system safely. Load one before changing that system's code.
   - `digests/`: one summary per week.

   Record folders, one file per source event, linked from the concept pages that cite them:

   - `prs/`, `issues/`, `incidents/`, `specs/` and `discussions/`.

   Concept pages cite their records in `sources`, and footnotes in the body point to them. Follow a footnote to check a claim.

3. Check `types/` for the fields a type uses before you read or write its frontmatter.
4. Read `log.md` for what changed recently, newest first.

## Add material

- Put new material in `inbox/`, one file per item, as Markdown. Notes, transcripts, pasted documents and links all go there. Ingest inbox turns them into records, and the refinement workflows update the concept pages from those.
- Don't edit concept pages directly. They're owned by workflows, and a direct edit is overwritten or skipped on the next run. If a page is wrong, add the correction to `inbox/` and say which page it's about.
- Don't edit records. They mirror their source.
- Make every change on a branch, never on `main`. People review and merge it.

## Write well

- Frontmatter links are bundle paths, like `/systems/billing-api.md`.
- Keep the type's folder: one type per folder.
- Never invent names. Use the names already in the repo.
