# xplor-debug

Diagnose and fix Xplor issues — root cause analysis, exact file location, complete fix.

## Usage
`/xplor-debug "<issue>"`

## Common Issues

### Progressive Disclosure Violations
```bash
/xplor-debug "API returning content.full at level 1"
/xplor-debug "sections appearing in scan response"
/xplor-debug "level field missing from node response"
```
Traces through the API route, finds where level stripping is broken, outputs exact fix.

### Broken Traversal
```bash
/xplor-debug "traverse returning empty path"
/xplor-debug "attention scores all returning 0"
/xplor-debug "traversal exceeding token budget"
```
Checks: graph loaded? start node exists? attention scoring working? token budget too small?

### Wikilink Parsing Failures
```bash
/xplor-debug "wikilinks not extracting from my markdown"
/xplor-debug "pipe aliases breaking wikilink parser"
/xplor-debug "anchor links #section not resolving"
```
Tests regex against your content, identifies edge cases (aliases, anchors, special chars).

### Graph Building Errors
```bash
/xplor-debug "duplicate node IDs in graph"
/xplor-debug "edges referencing non-existent nodes"
/xplor-debug "MOC clusters not being detected"
```

### Firebase / Firestore
```bash
/xplor-debug "saveProject failing with permission-denied"
/xplor-debug "Firestore quota exceeded on upload"
/xplor-debug "auth state not persisting after refresh"
```
Checks security rules, auth state, document structure, rate limits.

### Force Graph Rendering
```bash
/xplor-debug "graph canvas blank after upload"
/xplor-debug "nodes overlapping at simulation start"
/xplor-debug "edges not connecting to correct nodes"
```
Checks: data format, node/edge ID matching, simulation parameters, D3 force config.

### MCP Server
```bash
/xplor-debug "xplor mcp not connecting to Claude"
/xplor-debug "tool registration failing"
/xplor-debug "graph not loading in MCP context"
```
Checks: stdio transport, tool registration, graph file path, JSON serialization.

### CLI Errors
```bash
/xplor-debug "xplor index failing on TypeScript repo"
/xplor-debug "Tree-sitter WASM not loading"
/xplor-debug "graph file not saving to ~/.xplor/"
```

## Diagnostic Output Format

For every issue:

1. **Root cause** — what is actually broken and why
2. **Location** — exact file + line number
3. **Complete fix** — not a patch, a correct implementation
4. **Verification** — how to confirm the fix works

$ARGUMENTS
