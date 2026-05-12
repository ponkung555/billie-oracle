---
type: decision
status: active
date: 2026-05-09
---
# maw Over Raw tmux

**Decision**: `maw tmux send` is the canonical inter-agent channel. Raw `tmux send-keys` is banned for agent-to-agent communication.

## Why
- maw resolves fleet-stems (e.g., `jeans` → `01-jeans`) — no hardcoded session names needed
- `--force` flag bypasses any interactive confirmation prompts
- maw validates target existence before sending; raw tmux fails silently
- Centralises routing logic — if session naming ever changes, update fleet config, not every CLAUDE.md

## Boundary
This applies to agent-to-agent messages only. Raw `tmux send-keys` is still acceptable for one-off Poon-initiated shell operations.

## 🔗 Navigation
- Index: [[decision-index]]
- Related: [[agent-comm-protocol]]
