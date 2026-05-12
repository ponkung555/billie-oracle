---
type: bug-report
status: fixed
date-found: 2026-05-09
date-fixed: 2026-05-09
affected: annie-oracle
---
# 🐛 Session Not Running on First Contact

## What Broke
When Jeans attempted to route Report #2 to Annie via `maw tmux send --force annie "..."`, the message landed in a bare bash shell — no Claude Code running. Annie's tmux session (`50-enough`) didn't exist at all. The message was interpreted as a shell command: `Directive: command not found`.

## Root Cause
No session auto-start mechanism. Fleet configs define the session structure but don't launch it. `maw wake` only creates the session if missing — it doesn't launch Claude Code inside it. Jeans had no protocol to check agent readiness before sending.

## Fix
1. Added **Agent Communication Protocol** to `jeans-oracle/CLAUDE.md`:
   - Step 1: `maw panes` — confirm session exists and has active `claude` process
   - Step 2: If missing, `maw wake <agent>` → send `claude` → wait ~8s
   - Step 3: Then send directive via `maw tmux send --force`
2. Documented session name table (Jeans/Annie/Michael) in Jeans' CLAUDE.md

## Verification
Report #3 delivered with correct protocol — Annie was already running, directive landed cleanly.

## Lesson
Always run `maw panes` before sending a directive. The pane status shows both session existence and whether `claude` is the active command.

## 🔗 Navigation
- Index: [[bug-index]]
- Hub: [[../neverland-hub]]
- Related: [[../agents/annie]], [[../decisions/agent-comm-protocol]]
