---
type: decision
status: active
date: 2026-05-09
---
# Agent Communication Protocol

**Decision**: Jeans → agents go via `maw tmux send --force`. Agents → Jeans go via inbox file. Never tmux-send back to Jeans.

## Protocol — Jeans sending to agents (5 Steps)
1. `maw panes` — confirm session exists and shows active `claude` process
2. If missing: `maw wake <agent>` → `maw tmux send --force <session> "claude"` → wait ~8s
3. `maw tmux send --force <session> "<directive>"`
4. Immediately run `tmux send-keys -t <session> "" Enter` — paste-without-submit workaround
5. Check pane within 60s — if message still sits in `❯` unsubmitted, send one more empty Enter

## Protocol — agents acking Jeans
Agents write a file to `~/repos/jeans-oracle/ψ/inbox/ack-<agent>-<slug>.md`. Jeans reads inbox at session start. **No tmux-send back to Jeans.**

## Why
`maw tmux send` injects keystrokes directly into the target pane. When agents acked Jeans via tmux, it interrupted Jeans' live conversation with Poon — pasting agent text mid-prompt, or corrupting Poon's message. Inbox file acks are asynchronous and safe.

## Why (original)
Raw `tmux send-keys` silently misroutes when session names are wrong or agents aren't running. Discovered when Annie's ack to `51-jeans` failed silently — session didn't exist. `maw` resolves fleet-stems, validates targets, and `--force` bypasses interactive confirmation.

## Supersedes
Ad-hoc `tmux send-keys` calls in early session routing.

## 🔗 Navigation
- Index: [[decision-index]]
- Related bugs: [[../bugs/session-not-running]], [[../bugs/pane-naming-mismatch]], [[../bugs/double-enter-timing]]
