---
type: index
domain: neverland-operations
status: legacy
---
# 🏛️ Decision Index (Jeans Legacy)

| ID | Date | Decision | Rationale |
| :-- | :-- | :-- | :-- |
| [[agent-comm-protocol]] | 2026-05-09 | Use maw tmux send --force + pre-flight pane check | Raw tmux lost messages; maw gives fleet resolution + force flag |
| [[maw-over-raw-tmux]] | 2026-05-09 | Never use raw tmux send-keys for agent messages | maw resolves fleet-stems, handles force; raw tmux silently misroutes |
| [[enough-no-revision-loop]] | 2026-05-09 | Enough writes notes; Annie applies in next report | Revision loops create blocking dependencies; sequential is cleaner |
| [[enough-two-mode-closer]] | 2026-05-09 | Two-mode closer: That's enough vs Getting there | Long-term progress signal; single status collapsed editorial history |
| [[bypass-permissions-fleet]] | 2026-05-10 | bypassPermissions for all Claude Code agents | Permission prompts were stalling agents; Poon trusts the fleet |
| [[michael-time-vs-quota]] | 2026-05-10 | Michael uses output quotas, not time budgets | Michael has no clock; 10 minutes means nothing to him |
| [[inbox-watcher-architecture]] | 2026-05-10 | Event-driven watcher: detection (inotifywait) + relay (bash) + escalation (Jeans) | Scales to dev team; zero LLM cost for standard relay steps |

## ⚡ Billie's Orchestration Update
I am upholding these laws while expanding the fleet to include multi-model agents. The **Inbox-Ack Protocol** remains our primary coordination beat.

---
*Maintained by Billie (via Jeans).* 🕺✨⚖️
