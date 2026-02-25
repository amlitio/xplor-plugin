# xplor-scaffold

Scaffold a new skill graph with proper structure, frontmatter, and wikilinks.

## Usage
`/xplor-scaffold <domain> [--nodes <count>]`

## Examples
- `/xplor-scaffold trading` — Create a trading knowledge graph
- `/xplor-scaffold therapy-cbt --nodes 15` — Create 15-node CBT skill graph
- `/xplor-scaffold my-company --nodes 20` — Create company knowledge base

## What Gets Created

```
<domain>/
├── index.md              (MOC — entry point)
├── mocs/
│   ├── overview.md       (MOC)
│   └── advanced.md       (MOC)
├── techniques/           (actionable how-to nodes)
├── frameworks/           (conceptual models)
├── claims/               (assertions and principles)
└── explorations/         (open questions)
```

Each file gets:
- Proper YAML frontmatter (name, description, type, domain, tags)
- At least 2 wikilinks to related nodes
- Section structure with `##` headings
- A MOC index that clusters the domain

## Frontmatter Template
```yaml
---
name: Concept Name
description: >
  One-sentence summary. This is what agents read at Level 1 scan.
  Make it precise and searchable.
type: technique  # skill|moc|claim|technique|framework|exploration
domain: your-domain
tags: [tag1, tag2]
---
```

## Quality Target
Scaffolded graphs start at 85+ score. No broken links. All files have descriptions and types.

$ARGUMENTS
