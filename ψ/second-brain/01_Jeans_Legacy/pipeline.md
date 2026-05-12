---
type: reference
domain: neverland-operations
status: active
---
# 🔄 Research-to-Publication Pipeline

The full flow from Poon's request to a published Research Report.

```
Poon → Jeans
         ↓
   directive → Michael (/rrr+)
         ↓
   michael-oracle/ψ/second-brain/learnings/<slug>.md
         ↓
   Jeans picks topic from publishing-queue.md
         ↓
   directive → Annie (write + push)
         ↓
   directive → Nature (Thai localization)
         ↓
   Research-Report-by-Annie-N/README.md committed
         ↓
   directive → Enough (review + REVIEW.md)
         ↓
   Enough acks Jeans (title + closer signature)
         ↓
   Jeans tells Annie to read REVIEW.md before next assignment
         ↓
   Jeans logs milestone + marks queue complete
```

## Key Locations
| Asset | Path |
| :-- | :-- |
| Michael's learnings | `michael-oracle/ψ/second-brain/learnings/` |
| Publishing queue | `michael-oracle/ψ/second-brain/publishing-queue.md` |
| Annie's editorial memory | `annie-oracle/ψ/memory/learnings/` |
| Enough's review log | `enough-oracle/ψ/memory/reviews/review-log.md` |
| Article repos | `github.com/ponkung555/Research-Report-by-Annie-N` |

## Known Bug — Paste-Without-Submit
`maw tmux send --force` lands directive text but does not auto-submit at a fresh prompt. Always follow immediately with `tmux send-keys -t <session> Enter`. Confirmed on Annie and Enough — 2026-05-10.

## Permissions
All Claude Code agents (Jeans, Annie, Enough) now run with `"defaultMode": "bypassPermissions"`. No permission prompts. Michael uses Gemini CLI YOLO mode. Set 2026-05-10.

## Current Status
- Reports 1–4 shipped ([[milestones/reports-shipped|see milestones]])
- Full pipeline confirmed end-to-end: Annie → Report #4 → Enough → REVIEW.md ✓
- ARRA publish pipe for Michael still broken ([[bugs/arra-pipe-broken|tracked]])

## 🔗 Navigation
- Up: [[neverland-hub]]
- Team: [[team]]
