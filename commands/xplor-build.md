# xplor-build

Build a complete Xplor component from scratch — production-ready, Vercel-deployable.

## Usage
`/xplor-build <component>`

## Components

| Component | What Gets Built |
|-----------|----------------|
| `document-mode` | Full PDF upload → pdfjs-dist extraction → Claude entity extraction → Firestore persistence → Explorer |
| `skill-graph-mode` | ZIP ingestion → gray-matter frontmatter parsing → sentence-level wikilink extraction → MOC system → quality scoring |
| `code-mode` | Repo indexing → Tree-sitter WASM AST parsing → function/class/import entities → CALLS/IMPORTS/EXTENDS/DEFINES edges |
| `mcp-server` | All 8 MCP tools (query, context, impact, callers, callees, search, traverse, scan) via stdio transport |
| `explorer` | Mode-aware force-directed graph UI — document/code/skill/fused rendering, sidebar, progressive disclosure |
| `cli` | xplor index/mcp/serve/skill/fuse commands via commander.js, ~/.xplor/ graph storage |
| `api-routes` | All Next.js API routes: /api/extract, /api/share, /api/chat, /api/skillgraph/* |
| `agent-intelligence` | Attention scoring, traversal heuristics, telemetry, multi-domain fusion, context packing |
| `search` | Hybrid BM25 + cosine similarity + RRF fusion, field-weighted indexing |
| `auth` | Firebase Auth (Google + Email), AuthContext, Pro subscription gating via Stripe |

## What This Does

1. Reads the current codebase state — understands what exists, what's missing
2. Consults the GraphNode/GraphEdge canonical schema (graph-core)
3. Enforces progressive disclosure levels 0-4 and token budgets
4. Writes complete, tested, production-ready code — no TODOs, no stubs
5. Integrates with existing architecture without breaking other modes
6. Applies the dark theme design system (#0A0A0F, brand gradient, Space Grotesk)
7. Includes rate limiting, security controls, and error handling

## Quality Guarantees

- Node IDs: namespaced `skill:slug`, `code:path#Entity`, `doc:docId#entity-id`
- Every API response includes `level` field on every node
- `tokenBudget` is a hard ceiling — never exceeded
- Wikilinks use sentence-level context (not line-level)
- MOC nodes generate `CLUSTERS` edges (stronger than `REFERENCES`)

$ARGUMENTS
