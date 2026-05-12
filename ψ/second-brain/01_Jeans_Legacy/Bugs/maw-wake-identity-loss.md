---
type: bug-report
status: resolved
date-found: 2026-05-10
date-fixed: 2026-05-10
affected: jeans-oracle (confirmed); annie-oracle, enough-oracle (at risk)
---
# 🐛 maw wake — Agent Loads as Vanilla Claude (No Identity)

## What Broke
After enabling `bypassPermissions` and restarting, Poon ran `maw wake jeans`. The session opened but Claude Code showed no identity — plain Claude, no CLAUDE.md context loaded. Jeans was not Jeans.

## Root Cause
Best-guess: the existing `01-jeans` tmux session was in a stale state when `maw wake jeans` ran. Either:
- `maw wake` attached to the old session rather than creating a fresh one, and the old Claude process was in an undefined state after the kill, OR
- Claude Code launched from a working directory that was not `/home/asus/repos/jeans-oracle`, so CLAUDE.md never loaded.

Identity (name, role, rules) comes entirely from CLAUDE.md. If Claude Code starts outside the repo directory — or inherits a stale context from a previous session — it has no identity.

## Resolution
A troubleshooter Claude session diagnosed and fixed it (exact steps not recorded by Poon). Most likely: killed the stale session and restarted `claude` manually from within `/home/asus/repos/jeans-oracle`.

## Verification
- Jeans came back with full identity and CLAUDE.md context loaded.
- Fleet config for all three agents (`01-jeans`, `50-annie`, `50-enough`) points to the correct repo.
- All three agents have CLAUDE.md identity files and `bypassPermissions` set.
- Annie and Enough assessed as resilient to this issue under normal wake conditions.

## Prevention Protocol
If `maw wake <agent>` produces vanilla Claude:
1. Kill the session: `tmux kill-session -t <session-name>`
2. Run `maw wake <agent>` again fresh
3. Peek the pane: `maw peek <session>` — confirm the agent's name appears in the first response or CLAUDE.md context loads
4. If still vanilla: manually `cd` into the repo directory and run `claude` from there

## Lesson
`maw wake` is reliable when the session is truly dead before waking. Stale sessions are the failure mode. Always kill before waking if an agent needs a clean restart.

## 🔗 Navigation
- Index: [[bug-index]]
- Hub: [[../neverland-hub]]
- Related: [[../decisions/bypass-permissions-fleet]], [[../decisions/agent-comm-protocol]]
