---
type: decision
date: 2026-05-10
status: active
---
# Decision: Event-Driven Inbox Watcher — Foundation for Autonomous Pipeline

## What
A persistent shell watcher (`bin/inbox-watcher.sh`) runs in a dedicated tmux window (`01-jeans:watcher`) alongside Jeans' Claude pane. It watches `jeans-oracle/ψ/inbox/` via `inotifywait` and relays ack files to the next pipeline agent without Poon or Jeans needing to be in an active conversation.

## Architecture (three-layer separation)

| Layer | Owner | Tool | Cost |
| :-- | :-- | :-- | :-- |
| Detection | watcher script | inotifywait | zero — pure OS events |
| Decision (standard relay) | watcher script | bash logic | zero — no LLM |
| Decision (complex/non-standard) | Jeans (Claude) | Claude Code | tokens, on-demand |

### Standard relay rules (handled by watcher)
- `ack-annie-report-N.md` arrives → pre-flight check Enough → route review directive → log routing
- `ack-enough-report-N.md` arrives → log completion to `ψ/outbox/report-N-complete.md`

### Escalation to Jeans (future)
- Unknown ack file type → watcher logs but does not act
- Error recovery (agent not responding, bad commit) → watcher flags, Jeans decides

## Auto-start on maw wake jeans
Two changes to wire this permanently:

1. **`~/.config/maw/maw.config.json`** — `commands.watcher` → watcher script path
2. **`~/.config/maw/fleet/01-jeans.json`** — second window `watcher` with `repo: jeans-oracle`

From the next `maw wake jeans`, the watcher window auto-starts alongside the Claude pane.

## Why this over alternatives

| Alternative | Why rejected |
| :-- | :-- |
| Shell watcher only (no escalation path) | Can't handle complex decisions as team grows |
| Cron-scheduled Claude | Expensive (tokens every poll), imprecise timing, fragile |
| Jeans polls inbox manually | Requires Poon to be in conversation — not autonomous |
| File watcher with no-LLM relay | **Chosen** — cheap, always on, correct foundation for dev team scale |

## Long-term evolution path
1. **Now**: standard linear pipeline relay (Annie → Enough)
2. **Next**: `ψ/active/` state machine — track in-flight pipelines as a graph
3. **Future**: watcher handles parallel pipelines, escalates to Jeans for non-standard cases
4. **Dev team**: same architecture scales — watcher routes Coder, UX/UI acks the same way

## Key files
- `jeans-oracle/bin/inbox-watcher.sh` — the watcher
- `~/.config/maw/maw.config.json` — `commands.watcher` entry
- `~/.config/maw/fleet/01-jeans.json` — second window config

## 🔗 Navigation
- Index: [[decision-index]]
- Related milestone: [[../milestones/inbox-ack-protocol]]
- Related decision: [[agent-comm-protocol]]
