# xplor-debug

Debug Xplor issues — graph traversal problems, API errors, progressive disclosure violations.

## Usage
`/xplor-debug <issue>`

## Common Issues

### Progressive Disclosure Violations
`/xplor-debug "API returning content.full at level 1"`
Traces through the API route, identifies where the level stripping is missing,
outputs the exact fix.

### Broken Traversal
`/xplor-debug "traverse returning empty path"`
Checks: graph loaded correctly? start node exists? attention scoring returning 0?
token budget too small?

### Wikilink Parsing Failures
`/xplor-debug "wikilinks not extracting from my markdown"`
Tests the regex against your content, identifies edge cases (pipe aliases,
anchor links, special characters in filenames).

### Firebase/Firestore Errors
`/xplor-debug "saveProject failing with permission-denied"`
Checks security rules, auth state, document structure.

### Force Graph Not Rendering
`/xplor-debug "graph canvas blank after upload"`
Checks: data format, node/edge IDs match, simulation parameters.

### MCP Server Connection Failed
`/xplor-debug "xplor mcp not connecting to Claude"`
Checks: server transport, tool registration, graph loading.

## Diagnostic Output

For each issue, outputs:
1. Root cause analysis
2. Exact file and line number where the bug is
3. Complete fix (not a patch — a correct implementation)
4. How to verify the fix works

$ARGUMENTS
