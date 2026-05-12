---
type: bug-report
status: workaround
date-found: 2026-05-09
affected: all agents using maw tmux send
---
# 🐛 Double-Enter Timing — Message Sits Unsubmitted

## What Broke
When `maw tmux send --force <session> "message"` is called while the target agent's Claude Code is mid-response (generating output), the message lands in the input box but is not submitted. The Enter keystroke from `maw tmux send` is consumed by the outgoing output stream. The next time Jeans checks the pane, the message is visible in the `❯` prompt but needs another Enter to fire.

## Root Cause
Race condition: `maw tmux send` sends `tmux send-keys -t <target> '<message>' Enter`. When Claude Code is outputting text at the same moment, the Enter key event is absorbed before it can act as a submit on the typed message. This is a tmux/TUI timing issue, not a maw bug.

## Current Workaround
After sending a directive to an agent, check the pane. If the message is sitting in the `❯` input box without a response starting, run:
```
tmux send-keys -t <session> "" Enter
```
One empty Enter submits it. Takes ~5 seconds to confirm.

## Proper Fix (TODO)
- Option A: Add a brief `sleep 2` after `maw tmux send` in the protocol, then verify pane state
- Option B: maw could detect if the target is mid-response and queue the send until the pane goes idle
- Option C: Use `maw tmux send --literal` with a special newline sequence

Not blocking. The workaround is reliable. Fix when maw plugin work is scheduled.

## 🔗 Navigation
- Index: [[bug-index]]
- Hub: [[../neverland-hub]]
- Related: [[../decisions/agent-comm-protocol]]
