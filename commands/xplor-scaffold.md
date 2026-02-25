# xplor-scaffold

Scaffold a new skill graph with proper structure, frontmatter, and wikilinks — ready to score 85+.

## Usage
`/xplor-scaffold <domain> [--nodes <count>]`

## Examples
- `/xplor-scaffold trading` — Create a trading knowledge graph (~10 nodes)
- `/xplor-scaffold therapy-cbt --nodes 15` — Create 15-node CBT skill graph
- `/xplor-scaffold my-company --nodes 20` — Company knowledge base
- `/xplor-scaffold devops --nodes 12` — DevOps practices graph

## What Gets Created

```
<domain>/
├── index.md              (MOC — master entry point)
├── mocs/
│   ├── overview.md       (MOC — beginner cluster)
│   └── advanced.md       (MOC — advanced cluster)
├── techniques/           (actionable how-to nodes)
│   ├── <technique-1>.md
│   └── <technique-2>.md
├── frameworks/           (conceptual models)
│   └── <framework-1>.md
├── claims/               (assertions and principles)
│   └── <claim-1>.md
└── explorations/         (open questions)
    └── <exploration-1>.md
```

## Frontmatter Template

Every file gets proper YAML frontmatter:

```yaml
---
name: Concept Name
description: >
  One-sentence summary. This is what agents read at Level 1 scan.
  Make it precise and searchable.
type: technique  # skill | moc | claim | technique | framework | exploration
domain: your-domain
tags: [tag1, tag2]
---
```

## Wikilink Rules

- Every node gets at least **2 outgoing wikilinks** to related nodes
- MOCs link to 5-15 children (generating `CLUSTERS` edges)
- `extends:` and `contradicts:` frontmatter fields are used for typed edges
- Wikilinks include meaningful context sentences (not bare links)

## Quality Target

Scaffolded graphs start at **85+ score**:
- No broken links (all `[[targets]]` resolve to real files)
- All files have `description`, `type`, and `domain`
- MOCs cluster the domain properly
- No orphan nodes

## Node Density Guide

| Count | Structure |
|-------|-----------|
| 5-8 | 1 MOC, 1-2 techniques, 1 framework, 1 claim |
| 10-15 | 1 root MOC + 2 sub-MOCs, 4-6 techniques, 2 frameworks, 2 claims |
| 20+ | Full hierarchy: root → domain MOCs → leaf nodes across all types |

$ARGUMENTS
