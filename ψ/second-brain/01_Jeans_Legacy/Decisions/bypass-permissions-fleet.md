---
type: decision
date: 2026-05-10
status: active
---
# Decision: bypassPermissions for all Claude Code agents

## What
Set `"defaultMode": "bypassPermissions"` in `.claude/settings.json` (or `settings.local.json`) for Jeans, Annie, and Enough.

## Why
Permission prompts were blocking agent progress mid-task. Without Poon opening each terminal and approving manually, agents stalled silently. Poon granted full trust to the Claude Code fleet — equivalent to Gemini CLI's YOLO mode, which Michael already runs.

## Files Changed
- `annie-oracle/.claude/settings.json`
- `enough-oracle/.claude/settings.local.json`
- `jeans-oracle/.claude/settings.local.json`

## Applies Going Forward
New agents added to the fleet should receive `bypassPermissions` at birth.

## 🔗 Navigation
- Index: [[decision-index]]
