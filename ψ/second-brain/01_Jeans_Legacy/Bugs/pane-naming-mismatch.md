---
type: bug-report
status: fixed
date-found: 2026-05-09
date-fixed: 2026-05-09
affected: annie-oracle, jeans-oracle
---
# 🐛 Pane Naming Mismatch — Annie → Jeans Ack

## What Broke
When Annie completed a report, she ran `maw tmux send --force 51-jeans "..."` to ack Jeans. The session `51-jeans` does not exist. Jeans' actual session is `01-jeans`. The ack silently failed every time.

## Root Cause
Annie's `CLAUDE.md` was written with a hardcoded session name (`51-jeans`) that never matched the actual tmux session Jeans runs in (`01-jeans`). No fleet config existed for Jeans, so maw couldn't resolve it via fleet-stem either.

## Fix
1. Updated `annie-oracle/CLAUDE.md`: changed `51-jeans` → `01-jeans`
2. Created `~/.config/maw/fleet/01-jeans.json` — Jeans now resolvable via fleet-stem `jeans` OR exact `01-jeans`

## Verification
Annie's Report #3 ack: `✓ sent to 01-jeans → 01-jeans [fleet-stem (01-jeans)] (force)` — clean.

## Lesson
Every agent's CLAUDE.md must name exact session targets. When a new agent is born, verify the full ack chain before declaring them operational.

## 🔗 Navigation
- Index: [[bug-index]]
- Hub: [[../neverland-hub]]
- Related agents: [[../agents/annie]], [[../agents/jeans]]
