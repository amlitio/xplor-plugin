# xplor-validate

Validate a skill graph directory and output a quality score with actionable fixes.

## Usage
`/xplor-validate <path>`

## What This Does

Runs the full Xplor quality validation on a skill graph directory:

1. **Broken links** (-10 each): Finds all `[[wikilinks]]` pointing to non-existent files
2. **Missing descriptions** (-5 each): Files without `description` in YAML frontmatter
3. **Orphan nodes** (-3 each): Files with no incoming or outgoing links
4. **Missing type** (-2 each): Files without `type` in frontmatter
5. **Missing domain** (-1 each): Files without `domain` in frontmatter
6. **Circular-only** (-2 each): Node pairs that only link to each other

**Bonuses:**
- MOC coverage (+0 to +10): clusters that have a Map of Content node
- Link density health (+0 to +10): penalizes dead-end nodes

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

To reach 100:
  1. Create thought-journals.md or fix the link in cognitive-reframing.md
  2. Add description: to grounding-techniques.md frontmatter
  3. Add at least one link to/from case-formulation.md
```

$ARGUMENTS
