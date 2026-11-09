---
type: Type
title: Skill
description: An agent skill, as a folder with a SKILL.md that Claude or Codex can load.
schema:
  type: object
  properties:
    name:
      type: string
      pattern: '^[a-z0-9]+(-[a-z0-9]+)*$'
      maxLength: 64
      description: Skill name, matching its folder.
    license:
      type: string
      description: License of the skill.
    allowed-tools:
      type: string
      description: Tools the skill may use, space separated.
    metadata:
      type: object
      description: Extra key-value metadata.
    system:
      type: string
      pattern: '^/systems/[^/]+\.md$'
      description: System the skill is about.
  required: [name]
---

A Skill is a folder with a `SKILL.md` valid under the Agent Skills spec: `name` matches the folder, and `description` says what it does and when to use it. Other Markdown in the folder is a Reference. `type: Skill` is there until the engine treats `SKILL.md` as a Skill by filename, and strict Agent Skills validators may flag it.

- **Layer:** concept. Written by refinement workflows, which cite the records they read in `sources` and set `generated`. People review every change on its branch.
- **Folder:** `skills/*/`
- **Filenames:** `skills/<name>/SKILL.md`, like `skills/billing-api/SKILL.md`, with optional `skills/<name>/references/`.
- **Refined from:** Review feedback, systems and guides.

Example frontmatter:

```yaml
type: Skill
name: billing-api
description: How to change the Billing API safely. Use when working on charges, retries or invoices.
```
