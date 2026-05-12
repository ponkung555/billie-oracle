---
type: milestone
date: 2026-05-10
status: achieved
---
# Agents Talk Without Poon

**Date**: 2026-05-10  
**What happened**: Jeans routed a directive to Annie via `maw tmux send`. Annie responded by writing an ack file directly to `jeans-oracle/ψ/inbox/` — without Poon pressing Enter, without interrupting Jeans' conversation with Poon.

**Annie's ack**:
> *Hi-test received and ack'd — new protocol works. — Annie*

## Why This Matters

Before this session, every agent ack required Poon to manually enter a keystroke. The paste-without-submit bug meant Poon also had to watch panes and intervene when messages stalled. Agent-to-Jeans communication was not truly autonomous — it depended on Poon as a relay.

With the inbox-ack protocol:
- Agents write acks as files to `jeans-oracle/ψ/inbox/`
- No keystroke injection into Jeans' live pane
- No interruption of Jeans ↔ Poon conversation
- Jeans reads inbox at session start — fully async

**Neverland now has autonomous agent-to-agent communication.**

## What Changed
- `annie-oracle/CLAUDE.md` — ack step rewritten: write inbox file, never tmux-send to Jeans
- `enough-oracle/CLAUDE.md` — same
- `jeans-oracle/.claude/commands/route.md` — Enter fix baked in; inbox ack reminder added to every directive
- `ψ/second-brain/decisions/agent-comm-protocol.md` — protocol updated: one-way tmux (Jeans→agents), one-way inbox (agents→Jeans)

## 🔗 Navigation
- Index: [[milestone-index]]
- Related decision: [[../decisions/agent-comm-protocol]]
- Related bug fixed: [[../bugs/double-enter-timing]]
