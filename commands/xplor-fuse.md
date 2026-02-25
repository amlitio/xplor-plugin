# xplor-fuse

Merge multiple Xplor graphs (code + docs + skills) into a single queryable intelligence layer.

## Usage
`/xplor-fuse <sources>`

## Examples
```bash
# Fuse code graph with best-practices skill graph
/xplor-fuse --code ./my-repo --skills ./best-practices --output merged

# Fuse two skill graph domains
/xplor-fuse --skills ./cbt --skills ./attachment --output therapy-full

# Fuse code + docs + domain skills
/xplor-fuse --code ./repo --docs ./company-docs --skills ./onboarding --output company-full

# Fuse and inspect the result
/xplor-fuse --code ./repo --skills ./docs --output merged --validate
```

## What Fusion Does

1. **Loads** each graph from its source path or `~/.xplor/` store
2. **Prefixes** all node IDs with domain: `therapy:cognitive-distortions`, `code:src/auth.ts#login`
3. **Detects** same-name entities across domains → creates `CROSS_DOMAIN` edges
4. **Merges** into a single graph with all nodes and edges queryable together
5. **Saves** to `~/.xplor/<output>.json`

## Fusion Rules

| Condition | Action |
|-----------|--------|
| Same node ID across graphs | Merge metadata, union tags, keep both content versions |
| Same name, different domain | Create `CROSS_DOMAIN` edge with `weight: 0.7` |
| Conflicting descriptions | Keep both, flag in metadata as `conflicting: true` |
| Duplicate edges | Deduplicate, keep highest weight |

## Output Graph

The fused graph renders in Explorer with domain-colored background regions:
- Code domain: #61AFEF tinted region
- Skill domain: #FF9F43 tinted region
- Docs domain: #82E0AA tinted region
- `CROSS_DOMAIN` edges: thick dashed gold (#F7DC6F at 50% opacity)

## Fusion Storage

```
~/.xplor/
├── my-repo.json           # Code graph
├── best-practices.json    # Skill graph
└── merged.json            # Fused graph (both + CROSS_DOMAIN edges)
```

## Use Cases

- **Code + Docs**: Index your repo AND your company documentation — ask "which functions relate to the authentication policy?"
- **Code + Skills**: Repo + engineering best-practices — get style guidance while traversing call chains
- **Multi-domain Knowledge**: Fuse therapy modalities — CBT + attachment theory + somatic — into one traversable network
- **Onboarding Graph**: Company org + product knowledge + culture docs + codebase in one queryable layer

$ARGUMENTS
