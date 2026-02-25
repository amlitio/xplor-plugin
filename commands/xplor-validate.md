# xplor-validate

Validate a skill graph directory and output a quality score (0-100) with actionable fixes.

## Usage
`/xplor-validate <path>`

## Examples
- `/xplor-validate ./my-skills` — Validate a local skill graph directory
- `/xplor-validate ./therapy-cbt` — Score a domain-specific knowledge graph
- `/xplor-validate .` — Validate skill graph in current directory

## Scoring System

### Penalties
| Issue | Penalty | Detection |
|-------|---------|-----------|
| Broken wikilink | **-10** | `[[target]]` resolving to no file |
| Missing `description` | **-5** | YAML frontmatter without `description:` |
| Orphan node | **-3** | File with zero incoming AND outgoing links |
| Missing `type` | **-2** | Frontmatter without `type:` field |
| Missing `domain` | **-1** | Frontmatter without `domain:` field |
| Circular-only pair | **-2** | Node A and B only link to each other |

### Bonuses (max +20)
| Signal | Bonus |
|--------|-------|
| MOC coverage | +0 to +10 (clusters_with_moc / total_clusters × 10) |
| Link density health | +0 to +10 (penalizes dead-end nodes) |

## Output Format

```
Score: 87/100

Issues:
  ❌ broken-link: cognitive-reframing.md → [[thought-journals]] (not found) [-10]
  ⚠️  missing-description: grounding-techniques.md [-5]
  ⚠️  orphan: case-formulation.md (no connections) [-3]

Bonuses:
  ✅ MOC coverage: 3/4 clusters have MOC (+8)
  ✅ Link density: 1 dead end out of 24 nodes (+9)

Stats:
  Nodes: 24 | Edges: 47 | MOCs: 3 | Orphans: 1 | Broken links: 1

To reach 100:
  1. Create thought-journals.md or fix the link in cognitive-reframing.md
  2. Add `description:` to grounding-techniques.md frontmatter
  3. Add at least one link to/from case-formulation.md
```

## Notes

- Score is deterministic — same graph always produces same score
- Validation runs on the local filesystem (no server needed)
- Broken link detection is case-insensitive and handles spaces → hyphens

$ARGUMENTS
