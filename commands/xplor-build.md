# xplor-build

Build a complete Xplor component from scratch.

## Usage
`/xplor-build <component>`

## Examples
- `/xplor-build document-mode` — Build the full PDF upload → entity extraction → graph pipeline
- `/xplor-build skill-graph-mode` — Build ZIP ingestion, wikilink parsing, MOC system
- `/xplor-build mcp-server` — Build all 8 MCP tools (query, context, impact, traverse, scan, etc.)
- `/xplor-build explorer` — Build the mode-aware force-directed graph Explorer component
- `/xplor-build cli` — Build the xplor CLI (index, mcp, serve, skill, fuse commands)
- `/xplor-build api-routes` — Build all Next.js API routes (extract, share, chat, skillgraph/*)

## What This Does

Analyzes the current state of the codebase, identifies what needs to be built,
and produces complete, production-ready code that:

1. Conforms to the GraphNode/GraphEdge canonical schema from graph-core
2. Enforces progressive disclosure rules (levels 0-4, token budgets)
3. Integrates with the existing architecture without breaking other modes
4. Follows the dark theme design system (#0A0A0F, brand gradient, Space Grotesk)
5. Includes proper error handling, rate limiting, and security controls

All code is deployable to Vercel immediately.

$ARGUMENTS
