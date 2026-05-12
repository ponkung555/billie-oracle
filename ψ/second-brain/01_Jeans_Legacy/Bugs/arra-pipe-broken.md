---
type: bug-report
status: open
date-found: 2026-05-08
affected: michael-oracle
---
# 🐛 Michael's ARRA Publish Pipe — Broken

## What Broke
Michael (Gemini CLI) cannot POST to ARRA Oracle at `localhost:47778`. His `maw` transport layer returns `connection failed` when attempting to sync findings. Every attempt to push learnings to ARRA fails silently or with a connection error.

## Root Cause
Unknown. ARRA Oracle is running (accessible from Jeans' session). The failure appears specific to Michael's Gemini CLI environment and how it initialises the maw transport. Not yet debugged at the connection layer.

## Current Workaround
Jeans hand-delivers to ARRA on explicit request from Poon only. Default: skip ARRA sync, route directly from Michael's `second-brain/` filesystem. Annie and Enough read from filesystem — no ARRA dependency in the current pipeline.

## Impact
Low for current pipeline. All agents read Michael's notes from filesystem. ARRA is the visualisation/search layer — its absence doesn't block publication.

## To Fix
1. Compare maw transport config between Michael's session and Jeans'
2. Check if Gemini CLI has different environment variables for localhost resolution
3. Test `curl localhost:47778` from within Michael's tmux session

## 🔗 Navigation
- Index: [[bug-index]]
- Hub: [[../neverland-hub]]
- Related: [[../agents/michael]]
