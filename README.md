# Xplor — Claude Code Plugin

**Structured cognition engine for Claude Code.** Transforms documents, codebases,
and knowledge systems into traversable, AI-queryable knowledge graphs.

## Install

```bash
# Add the Xplor marketplace
/plugin marketplace add amlitio/xplor-plugin

# Install the plugin
/plugin install xplor@xplor
```

Or from a local directory:
```bash
/plugin marketplace add ./xplor-plugin
/plugin install xplor@xplor
```

## What You Get

### 🤖 xplor-expert Agent
A senior engineer with complete mastery of the Xplor platform. Knows every spec,
every API contract, every design decision. Activate conversationally:

> "Build the skill graph ingestion pipeline"
> "Fix the progressive disclosure violation in the traverse endpoint"
> "Add fusion support to the Explorer component"

### 📚 Skill
The complete Xplor specification loaded as a Claude Code skill. Claude will
automatically reference this when working on any Xplor component.

### ⚡ Commands

| Command | What It Does |
|---------|-------------|
| `/xplor-build <component>` | Build a complete Xplor component from scratch |
| `/xplor-validate <path>` | Validate a skill graph, score it 0-100, list fixes |
| `/xplor-scaffold <domain>` | Scaffold a new skill graph with proper structure |
| `/xplor-debug <issue>` | Diagnose and fix Xplor bugs with root cause analysis |
| `/xplor-fuse <sources>` | Merge multiple graphs (code + docs + skills) into one |

## Three Modes

```
Document Mode   — PDFs → entities → knowledge graph (Claude API extraction)
Code Mode       — Repos → AST → call-chain graphs (Tree-sitter parsing)  
Skill Graph Mode — Markdown + wikilinks → navigable intelligence graphs
```

All three feed into the same Explorer UI. All three can be fused into a single
queryable intelligence layer.

## Quick Start

```bash
# Validate your skill graph
/xplor-validate ./my-skills

# Scaffold a new domain
/xplor-scaffold trading --nodes 20

# Build a component
/xplor-build skill-graph-mode

# Debug an issue
/xplor-debug "wikilinks not extracting"
```

## Quick Start

```bash
# Validate your skill graph
/xplor-validate ./my-skills

# Scaffold a new domain
/xplor-scaffold trading --nodes 20

# Build a component
/xplor-build skill-graph-mode

# Debug an issue
/xplor-debug "wikilinks not extracting"

# Fuse graphs across domains
/xplor-fuse --code ./repo --skills ./best-practices --output merged
```

## Stack

Next.js 14 · Firebase · Claude claude-sonnet-4-6 API · Tree-sitter · gray-matter · MCP SDK · Stripe · Vercel

## Links

- **Web App**: https://file-xplor.vercel.app
- **GitHub**: https://github.com/amlitio/xplor-plugin
- **Docs**: See `skills/xplor/SKILL.md` for the complete specification
