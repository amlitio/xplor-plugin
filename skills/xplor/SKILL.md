---
name: xplor
description: >
  Build Xplor — a structured cognition engine that transforms documents, codebases, and
  knowledge systems into traversable, AI-queryable knowledge graphs. Three modes:
  (1) Document Mode — PDFs to entity/relationship graphs with AI extraction.
  (2) Code Mode — repositories to function/class/call-chain graphs via AST parsing.
  (3) Skill Graph Mode — structured markdown knowledge systems with wikilinks, YAML
  frontmatter, and Maps of Content into navigable intelligence graphs for AI agents.

  Use this skill whenever the user wants to: build a knowledge graph platform, create a
  document intelligence tool, analyze codebases, build an MCP server for code or knowledge,
  create a skill graph engine, build agent cognition infrastructure, create a CLI for
  indexing repos or knowledge bases, build structured knowledge systems, create traversable
  skill networks with wikilinks, build something like DeepWiki but deeper, build "git for
  structured knowledge", create a "graph OS" for AI agents, or anything involving knowledge
  graphs + AI agents + structured traversal.

  Also trigger for: Next.js + Firebase + AI extraction, force-directed graph UIs, AST
  parsing with Tree-sitter, MCP server development, wikilink parsing, YAML frontmatter
  extraction, skill authoring tools, agent traversal telemetry, attention scoring,
  progressive disclosure systems, or multi-domain graph fusion. Even partial matches like
  "skill graph", "knowledge engine", "structured cognition", "agent context", "code
  explorer", "repo intelligence" should trigger this skill.
---

# Xplor — Structured Cognition Engine

> People underestimate the power of structured knowledge. Structured knowledge enables
> entirely new classes of applications.

Xplor transforms **documents**, **codebases**, and **knowledge systems** into traversable,
queryable knowledge graphs — then exposes them to AI agents so they don't just follow
instructions, they **understand domains**.

## Why Xplor Exists

Traditional tools give you descriptions. Xplor gives you **relationships**.

When an AI agent asks "What uses this function?" — it gets call chains, downstream
impacts, execution flows. When it asks "How does this therapy technique connect to
attachment theory?" — it traverses the skill graph and pulls in exactly what the
situation requires.

This is the difference between an agent that follows instructions and an agent that
understands a domain.

## Three Modes

| Mode | Input | Extraction Method | Graph Contains |
|------|-------|------------------|----------------|
| **Document** | PDFs, text files | AI entity extraction (Claude) | People, orgs, locations, dates, concepts + relationships |
| **Code** | Git repos, ZIP, local paths | AST parsing (Tree-sitter) | Functions, classes, imports, call chains + CALLS/IMPORTS/EXTENDS/DEFINES |
| **Skill Graph** | Markdown with wikilinks | Structural parsing (frontmatter + links) | Knowledge nodes, MOCs, claims, techniques + semantic connections |

All three modes feed into the same **Knowledge Graph Core** and render through the same
**Explorer UI**. They can also be **fused** — code graph + company docs + domain skills
merged into a single queryable intelligence layer.

---

## Architecture

```
Xplor Platform
├── Interfaces
│   ├── Web UI (Next.js — upload, explore, chat, skill graph browser)
│   ├── CLI (xplor index, xplor mcp, xplor serve, xplor skill)
│   └── MCP Server (query, context, impact, traverse, search)
│
├── Ingestion Pipelines
│   ├── Document Pipeline (PDF → text → AI entity extraction)
│   ├── Code Pipeline (repo → AST → nodes/edges via Tree-sitter)
│   └── Skill Graph Pipeline (markdown → frontmatter + wikilinks → knowledge graph)
│
├── Knowledge Graph Core
│   ├── In-memory graph (nodes + edges + metadata)
│   ├── Traversal engine (BFS/DFS + attention scoring + depth limits)
│   ├── Search (BM25 full-text + semantic similarity)
│   └── Progressive disclosure (index → descriptions → links → sections → full)
│
├── Agent Intelligence Layer
│   ├── Traversal heuristics (attention scoring, path ranking)
│   ├── Context injection (pull relevant nodes for current task)
│   ├── Telemetry (which nodes loaded, why, what was skipped)
│   └── LLM augmentation (Claude API for enrichment + chat)
│
└── Deployment
    ├── Vercel (web app)
    └── npm package (CLI + MCP server)
```

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 14 (App Router) |
| Auth | Firebase Auth (Google + Email) |
| Database | Cloud Firestore + in-memory graph |
| AI | Anthropic Claude API |
| PDF Parsing | pdfjs-dist (client-side) |
| Code Parsing | Tree-sitter (WASM for web, native for CLI) |
| Markdown Parsing | gray-matter (frontmatter) + custom wikilink parser |
| MCP Server | @modelcontextprotocol/sdk |
| CLI | commander.js |
| Payments | Stripe |
| Hosting | Vercel + npm registry |

---

## Build Phases

Build in this order. Each phase is independently deployable.

### Phase 1: Document Mode (Web App)
Upload PDFs → AI extracts entities → interactive knowledge graph.
See document-mode reference below.

### Phase 2: Code Mode (Ingestion + CLI)
Index repos via AST parsing, build call-chain graphs.
See code-mode and cli-spec references below.

### Phase 3: MCP Server
Expose the graph to AI agents via Model Context Protocol.
See mcp-server-spec reference below.

### Phase 4: Skill Graph Mode
Transform structured markdown into navigable intelligence graphs.
See skill-graph-spec reference below.

### Phase 5: Agent Intelligence Layer
Traversal heuristics, telemetry, progressive disclosure, multi-domain fusion.
See agent-intelligence reference below.

---

## Design System

### Color Palette

```javascript
// Backgrounds
// Page:    #0A0A0F  (near-black with blue undertone)
// Surface: rgba(255,255,255, 0.03)
// Brand:   linear-gradient(135deg, #FF6B6B, #4ECDC4)

const TYPE_COLORS = {
  // Document entities
  person: "#FF6B6B", organization: "#4ECDC4", location: "#45B7D1",
  date: "#F7DC6F", money: "#BB8FCE", concept: "#82E0AA",
  document: "#F0B27A", event: "#AED6F1",
  // Code entities
  function: "#61AFEF", class: "#C678DD", variable: "#E5C07B",
  import: "#56B6C2", module: "#98C379", file: "#ABB2BF",
  // Skill graph entities
  skill: "#FF9F43", moc: "#EE5A24", claim: "#A3CB38",
  technique: "#FDA7DF", framework: "#9AECDB", exploration: "#7158e2",
  default: "#636e72",
};
```

### Typography
- Headings: 'Space Grotesk', sans-serif
- Body: 'Outfit', system-ui, sans-serif
- Dark-first, minimal chrome. The graph is the hero.

---

## Graph Core — Canonical Data Model

**Rule: If it's a node or edge in Xplor, it conforms to this schema. No exceptions.**

```typescript
type GraphKind = "document" | "code" | "skill" | "fused";

interface GraphNode {
  id: string;           // Namespaced: "skill:cognitive-reframing", "code:src/auth.ts#login"
  kind: GraphKind;
  type: string;         // person|org|function|class|skill|moc|technique|framework|claim|exploration
  name: string;
  description?: string;
  domain?: string;
  tags?: string[];
  source?: {
    filePath?: string;
    repo?: string;
    documentId?: string;
    startLine?: number;
    endLine?: number;
    updatedAt?: string;
  };
  content?: {
    full?: string;        // Level 4: complete content
    sections?: SectionPreview[];  // Level 3: headers + first paragraph
  };
  metadata?: {
    wordCount?: number;
    inDegree?: number;
    outDegree?: number;
    signature?: string;
    language?: string;
    aliases?: string[];
  };
}

interface GraphEdge {
  id: string;
  kind: GraphKind;
  type: "REFERENCES"|"CLUSTERS"|"EXTENDS"|"CONTRADICTS"|"CALLS"|"IMPORTS"|"DEFINES"|"USES"|"EXPORTS"|"RELATED_TO"|"CROSS_DOMAIN";
  source: string;
  target: string;
  label?: string;
  context?: string;   // Sentence containing the link/call
  weight?: number;
  domain?: string;
}
```

### Node ID Rules
- Skill nodes: `skill:slug-from-filename`
- Code nodes: `code:src/path/file.ts#EntityName`
- Document nodes: `doc:documentId#entity-id`
- Lowercase, hyphens, strip `.md`, slugify special chars

---

## Progressive Disclosure — Enforcement Rules

**Mandatory for every interface: Web API, CLI, MCP tools.**

| Level | Name | What's Returned | What's Forbidden |
|-------|------|----------------|------------------|
| 0 | Index | Node IDs, names, domains, types, MOC list | Any content, descriptions, links |
| 1 | Scan | Frontmatter only: id, name, type, domain, description, tags | Markdown body, sections, links, full content |
| 2 | Links | Link targets + context sentences + target descriptions | Section previews, full content |
| 3 | Sections | Headings + first paragraph per section (~100 words each) | Full content body |
| 4 | Full | Complete markdown/code content | Nothing forbidden |

### Enforcement
- Every node returned must include `level` field
- Forbidden fields are NEVER included — violations are bugs
- `tokenBudget` is a hard ceiling; stop loading before exceeding it
- Every API call emits telemetry: `{ nodesVisited, nodesLoaded, nodesAtLevel, tokensUsed }`

---

## Document Mode Implementation

### Files to Build (in order)
1. `lib/firebase.js` — Firebase init, saveProject, getProjects, deleteProject, logOut
2. `lib/AuthContext.js` — React context wrapping Firebase auth state
3. `app/layout.js` — Root layout with AuthProvider, dark theme globals, Google Fonts
4. `components/AuthScreen.js` — Login/signup with Google + email
5. `components/ProjectsDashboard.js` — Grid of saved projects with delete
6. `components/UploadScreen.js` — PDF drop zone → pdfjs-dist client-side extraction
7. `app/api/extract/route.js` — POST endpoint calling Claude for entity extraction
8. `components/Explorer.js` — Force-directed graph + sidebar + list view
9. `app/page.js` — Screen router: landing → auth → dashboard → upload → explorer
10. `components/ShareButton.js` — Public share links
11. `app/shared/[id]/page.js` — Public viewer (no auth, view counter, CTA)
12. `app/api/share/route.js` — Share CRUD
13. `components/NetworkChat.js` — AI Q&A floating panel (Pro feature)
14. `app/api/chat/route.js` — Chat endpoint
15. Stripe integration — checkout, webhooks, Pro gating

### AI Entity Extraction Prompt
```
You are an entity extraction engine. Analyze the text and return ONLY valid JSON.
Extract entities (people, organizations, locations, dates, monetary amounts, concepts,
documents, events) and connections between them.

Return format:
{
  "entities": [
    { "id": "unique-id", "name": "Entity Name", "type": "person|organization|location|date|money|concept|document|event", "description": "Brief description" }
  ],
  "connections": [
    { "source": "entity-id-1", "target": "entity-id-2", "label": "relationship description" }
  ]
}

Be thorough. Extract 10-30 entities per chunk. Include cross-references.
```

Use `claude-sonnet-4-20250514`. max_tokens: 4096.
PDF chunking: ~14,000 chars per chunk, up to 6 chunks.

### Firestore Schema
```
users/{uid}/projects/{projectId}:
  name, entities[], connections[], documents[], documentNames[],
  entityCount, connectionCount, documentCount, createdAt, updatedAt

shared_projects/{shareId}:
  name, entities[], connections[], entityCount, connectionCount,
  documentCount, sharedBy, sharedAt, views, ownerUid

users/{uid}/subscription:
  status, stripeCustomerId, stripePriceId, currentPeriodEnd
```

---

## Code Mode — AST Ingestion Pipeline

### File Discovery
```javascript
import { glob } from "glob";
const LANGUAGE_MAP = {
  ".js": "javascript", ".jsx": "javascript",
  ".ts": "typescript", ".tsx": "typescript",
  ".py": "python",
};
const IGNORE = ["**/node_modules/**", "**/dist/**", "**/.git/**", "**/*.min.js"];
```

### Entity Extraction from AST

| AST Node | Entity Type | Fields |
|----------|------------|--------|
| `function_declaration` | function | name, params, return type, line range |
| `arrow_function` (assigned) | function | name from variable, params |
| `method_definition` | function | name, class, params |
| `class_declaration` | class | name, extends, methods |
| `import_statement` | import | source, specifiers |

### Relationships

| Relationship | How Detected |
|-------------|-------------|
| CALLS | `call_expression` where callee matches known function |
| IMPORTS | `import_statement` resolved to target file |
| EXTENDS | `class_declaration` with superclass |
| DEFINES | Function/class found inside file |

---

## Skill Graph Mode — Full Implementation

### Ingestion Pipeline

**Step 1** — Walk directory for `.md` files. Ignore: `.git`, `node_modules`, `dist`, `.next`, `build`.

**Step 2** — Parse YAML with `gray-matter`. Required: `description`. Optional: `name`, `type`, `domain`, `tags`, `aliases`, `extends`, `contradicts`.

**Step 3** — Wikilink extraction with sentence-level context:
```javascript
function extractWikilinks(content) {
  const sentences = content.match(/[^.!?\n]+[.!?\n]+/g) || [content];
  const links = [];
  for (const sentence of sentences) {
    const re = /\[\[([^\]|#]+)(?:#([^\]|]+))?(?:\|([^\]]+))?\]\]/g;
    let match;
    while ((match = re.exec(sentence)) !== null) {
      links.push({
        target: slugify(match[1].trim()),
        anchor: match[2] || null,
        alias: match[3] || null,
        contextSentence: sentence.trim(),  // sentence, NOT full line
      });
    }
  }
  return links;
}

function slugify(str) {
  return str.toLowerCase().replace(/\.md$/, "").replace(/\s+/g, "-").replace(/[^a-z0-9-]/g, "");
}
```

**Step 4** — Node construction:
```javascript
{
  id: `skill:${slug}`,
  kind: "skill",
  type: frontmatter.type || "skill",
  name: frontmatter.name || titleFromFilename,
  description: frontmatter.description,
  domain: frontmatter.domain || "general",
  tags: frontmatter.tags || [],
  source: { filePath: relativePath, updatedAt: stat.mtime },
  content: { full: markdownBody, sections: extractSections(markdownBody) },
  metadata: { wordCount: markdownBody.split(/\s+/).length, aliases: frontmatter.aliases || [] },
}
```

**Step 5** — Edge rules:
| Condition | Edge Type |
|-----------|----------|
| Default wikilink | `REFERENCES` |
| Source node type is `moc` | `CLUSTERS` |
| Declared in frontmatter `extends: [...]` | `EXTENDS` |
| Declared in frontmatter `contradicts: [...]` | `CONTRADICTS` |

### Maps of Content (MOCs)
- Identified by `type: moc` in frontmatter
- Should link to 5-15 children
- Wikilinks in MOCs generate `CLUSTERS` edges (stronger than `REFERENCES`)
- 1 MOC per 5-10 skill nodes is healthy

### MOC Example
```markdown
---
name: cbt-techniques
description: Map of Content for CBT techniques. Entry point for agent traversal.
type: moc
domain: therapy
---

# CBT Techniques

## Cognitive Techniques
- [[cognitive-reframing]] — challenging distorted thoughts
- [[thought-records]] — structured thought analysis worksheets
- [[cognitive-distortions]] — taxonomy of common patterns
```

---

## Skill Graph Quality Scoring

Score: 0-100. Deterministic — same graph always produces same score.

### Penalties
| Issue | Penalty |
|-------|---------|
| Broken wikilink | **-10** per link |
| Missing `description` in frontmatter | **-5** per file |
| Orphan node (no links) | **-3** per node |
| Missing `type` | **-2** per file |
| Missing `domain` | **-1** per file |
| Circular-only reference (A↔B isolated) | **-2** per pair |

### Bonuses (max +20)
| Signal | Bonus |
|--------|-------|
| MOC coverage | +0 to +10 (clusters_with_moc / total_clusters * 10) |
| Link density health | +0 to +10 (penalize dead ends) |

---

## Skill Graph Web API

### POST /api/skillgraph/ingest
Upload ZIP or GitHub URL → parse markdown → build graph.
Returns: `{ graphId, kind, metrics, validation }`

### POST /api/skillgraph/scan
Frontmatter-only search. Returns Level 1 data — **never** returns markdown body.
Returns: `{ results: [{id, name, type, domain, description, tags, inDegree, outDegree}], level: 1 }`

### POST /api/skillgraph/traverse
Navigate graph with attention scoring.
Request: `{ graphId, startNode, query, maxDepth: 3, maxNodes: 8, tokenBudget: 6000 }`
Returns: `{ entryPoint, path: [{id, name, level, content, score, reason}], unloaded, telemetry }`

### POST /api/skillgraph/context
Assemble optimal context pack for a query.
Request: `{ graphId, query, tokenBudget: 6000 }`
Returns: `{ contextPack: { entryPoint, nodes: [{id, level, content, tokens}], totalTokens }, telemetry }`

### POST /api/skillgraph/validate
Run quality validation.
Returns: `{ score, issues: {brokenLinks, missingDescriptions, orphans}, bonuses, summary }`

### GET /api/skillgraph/stats?graphId=X
Returns: `{ nodeCount, edgeCount, density, avgDegree, typeBreakdown, clusterCount, orphanCount }`

---

## Agent Intelligence Layer

### Attention Scoring
```javascript
function computeAttentionScore(node, query, graph) {
  let score = 0;
  // Semantic relevance (0-40)
  score += semanticSimilarity(node.description + " " + node.name, query) * 40;
  // Graph centrality (0-20)
  const inDegree = graph.edges.filter(e => e.target === node.id).length;
  const outDegree = graph.edges.filter(e => e.source === node.id).length;
  score += Math.min(20, (inDegree + outDegree) * 2);
  // Type bonus: moc=+15, framework=+10, technique=+5
  if (node.type === "moc") score += 15;
  if (node.type === "framework") score += 10;
  if (node.type === "technique") score += 5;
  // Recency (0-10)
  if (node.updatedAt) {
    const days = (Date.now() - new Date(node.updatedAt)) / 86400000;
    score += Math.max(0, 10 - days * 0.1);
  }
  return Math.min(100, score);
}
```

### Traversal Pattern
```
Agent receives task
  → Index (Level 0): what MOCs exist?
  → Scan (Level 1): which nodes match the task?
  → Links (Level 2): what's connected to the matches?
  → Sections (Level 3): confirm relevance with previews
  → Full (Level 4): load 3-8 most relevant nodes
  → Assemble context pack within token budget
```

### Multi-Domain Fusion
Merge multiple graphs into one queryable layer:
- Domain prefix all IDs: `therapy:cognitive-distortions`
- Detect same-name entities across domains → create `CROSS_DOMAIN` edges
- Use cases: Code + Docs, Code + Skills, Company Knowledge (org + product + culture)

---

## MCP Server — 8 Tools

```javascript
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import { z } from "zod";

// Tools:
// query(question)       — Find entities by description
// context(symbol)       — Deep context + all relationships
// impact(target)        — Downstream dependency analysis
// callers(fn, depth)    — Upstream call chain
// callees(fn, depth)    — Downstream call chain
// search(query, limit)  — Full-text search
// traverse(startNode, query, maxDepth, maxNodes) — Skill graph traversal
// scan(query, domain)   — Frontmatter-only scan (Level 1)
```

### Agent Configuration
`~/.claude/claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "xplor": { "command": "xplor", "args": ["mcp"] }
  }
}
```

---

## CLI Spec

```bash
# Core
xplor index <path>               # Index a repo (local path, GitHub URL, or ZIP)
xplor index ./repo --languages js,ts
xplor mcp                        # Start MCP server (stdio transport)
xplor serve                      # Start web UI locally
xplor query "find auth functions"
xplor impact src/auth/validate.ts

# Skill Graph
xplor skill init <name>
xplor skill validate <path>
xplor skill stats <path>
xplor skill viz <path> --open

# Fusion
xplor fuse --code ./repo --skills ./best-practices --output merged
xplor fuse --skills ./cbt --skills ./attachment --output therapy-full
```

### Graph Storage
```
~/.xplor/
├── config.json
└── graphs/
    ├── my-project.json        # Code graph
    ├── therapy-cbt.json       # Skill graph
    └── merged-full.json       # Fused graph
```

---

## Search — Hybrid BM25 + Semantic

```javascript
// Scoring formula:
finalScore = 0.6 * BM25_score + 0.3 * cosine_similarity + 0.1 * degreeBoost

// Fields indexed:
// name (weight 3.0), description (2.0), tags (1.5)
// skill: section headings (1.5), section previews (1.0)
// code: signature (2.0), filePath (1.0)
// content.full NOT indexed by default (too noisy)

// Reciprocal Rank Fusion when both BM25 and semantic available:
function reciprocalRankFusion(bm25Results, semanticResults, k = 60) {
  const scores = {};
  bm25Results.forEach((id, rank) => scores[id] = (scores[id]||0) + 1/(k+rank+1));
  semanticResults.forEach((id, rank) => scores[id] = (scores[id]||0) + 1/(k+rank+1));
  return Object.entries(scores).sort(([,a],[,b]) => b-a).map(([id]) => id);
}
```

---

## Security & Limits

| Limit | Value |
|-------|-------|
| Max ZIP upload | 10 MB |
| Max file count | 500 files |
| Max total markdown | 5 MB |
| Max PDF size | 25 MB |
| Max PDFs per upload | 10 |
| Ingestion rate | 20 req/hour/user |
| AI extraction | 60 chunks/hour/user |
| AI chat | 30 msg/hour (Pro: 120) |

### Pro Feature Gating ($9.99/mo)
| Feature | Free | Pro |
|---------|------|-----|
| PDF uploads | 3/day | Unlimited |
| AI chat | ❌ | ✅ |
| Code Mode | 1 repo/day | Unlimited |
| Skill Graph Mode | 1 graph/day | Unlimited |
| Multi-domain fusion | ❌ | ✅ |
| Traversal telemetry | Basic | Full with export |

---

## Explorer Component Architecture

```typescript
interface ExplorerProps {
  data: {
    kind: "document" | "code" | "skill" | "fused";
    nodes: GraphNode[];
    edges: GraphEdge[];
    metrics?: GraphMetrics;
  };
  onBack: () => void;
}
```

### Node Rendering by Mode
- **Document**: Circle, radius proportional to connections, entity type color
- **Code**: Rounded rectangle (functions/classes), circle (files/imports), dashed border for external
- **Skill**: Rectangular card (~120x50px), larger bordered rectangle for MOCs + glow
- **Fused**: Domain-colored background regions, `CROSS_DOMAIN` edges = thick dashed gold

### Edge Styles
| Type | Style | Color |
|------|-------|-------|
| REFERENCES | Solid | rgba(255,255,255,0.1) |
| CLUSTERS | Solid | #EE5A24 at 30% |
| CALLS | Dashed | #61AFEF at 30% |
| CROSS_DOMAIN | Thick dashed | #F7DC6F at 50% |

### Sidebar Tabs
- **Info**: name, type badge, domain, description, source
- **Links**: outgoing + incoming (clickable navigation)
- **Sections**: `content.sections[]` previews + "Load Full" button
- **Full**: complete `content.full` as markdown/syntax-highlighted code
- **Telemetry** (skill mode): attention score, level loaded, reason, traversal position

---

## Example Skill Graph Structures

### Therapy (CBT)
```
therapy-cbt/
├── index.md (moc)
├── techniques/
│   ├── cognitive-reframing.md → [[thought-records]], [[cognitive-distortions]]
│   ├── thought-records.md → [[socratic-questioning]]
│   └── exposure-hierarchy.md → [[behavioral-activation]]
├── claims/
│   └── validation-first.md → [[grounding-techniques]]
└── frameworks/
    └── case-formulation.md
```

### Company Knowledge
```
acme-corp/
├── index.md (moc)
├── mocs/org-structure.md, product-knowledge.md, processes.md, culture.md
├── products/widget-pro.md, pricing-model.md
├── processes/incident-response.md, deployment-pipeline.md
└── culture/decision-making.md, values.md
```
