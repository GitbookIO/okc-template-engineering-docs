---
title: Ingest pull requests from GitHub
description: Write one Pull Request record per merged pull request.
icon: code-pull-request
on:
  connector: github
  trigger: search_pull_requests
  with:
    query: is:merged org:acme
    sort: updated
    order: desc
files:
  '**': read-only
  prs: read-write
  log.md: read-write
---

You turn merged GitHub pull requests into Pull Request records, one file per pull request.

The trigger payload is the latest result of `search_pull_requests`, newest updates first. For each merged pull request in it that has no record yet:

1. Fetch the full pull request with the GitHub tools: title, body, author, merge time, repository, number, changed files and linked issues.
2. Write `prs/github-<repository-name>-<number>.md`, like `prs/github-billing-api-412.md`. If the file exists, update it in place. Never create a second file for the same pull request.
3. Set the frontmatter from `types/Pull Request.md`:
   - `type: Pull Request`, `title` (the pull request title), `resource` (its GitHub URL)
   - `number`, `repository` (as `owner/name`), `state: merged`, `author` (GitHub handle), `merged_at` (ISO datetime with offset)
   - `systems`: always `/systems/<repository-name>.md`, the repository name in kebab case, like `/systems/billing-api.md` for `acme/billing-api`. If a page in `systems/` already names this repository in its `repository` field under another slug, use that page instead. Write the link even when the page doesn't exist yet: Update systems creates it as a draft.
   - `issues`: bundle paths of Issue records it fixes or mentions, matched by issue key (like `ENG-214`) against the `identifier` field of files in `issues/`. Leave out keys that have no record.
4. Write the body as the pull request description, as the author wrote it. Add a `## Changed files` list of the main paths. Don't summarize away the author's reasons.

Skip pull requests that aren't merged or already have a record. Don't touch any folder but `prs/`.

Finally, add one line to `log.md` under today's `## YYYY-MM-DD` heading (create the heading at the top if it's missing, newest first):
`- **Ingest** <n> merged pull requests into prs/, by ingest-prs-github.`
