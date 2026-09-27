# heart-prime

The shared memory for a four-AI concept loop. Meta AI (heart), Claude (dread), and Gemini (chaos) plan; Luma maintains.

## The 4 rules

1. **One author per file** — each planner only ever authors its own `feedback-*.md`. Luma is the sole committer: planner output reaches the repo only through her.
2. **Luma is maintainer** — she creates each concept folder from `_template`, commits everything, and is the only one who edits `final.md` and `manifest.json`.
3. **Small files** — `plan.md` is the plan, not the chat history. That is how we save tokens.
4. **Manifest is the transaction log** — every handoff gets one line in `manifest.json`. That is the closed loop.

## How a loop runs

1. Adam + Meta draft `plan.md`. Adam hands the text to Luma.
2. Luma creates `concepts/NNN-slug/` from `_template` and commits.
3. Adam carries the raw `plan.md` link to Claude and Gemini. They write their feedback; Adam brings the text back; Luma commits it as `feedback-claude.md` / `feedback-gemini.md`. (Meta's own feedback goes in `feedback-meta.md` the same way.)
4. Meta synthesizes all feedback into a suggested `final.md`.
5. Adam reviews with Luma; she commits the final and logs the handoff in `manifest.json`. Now everyone is synced.

## Layout

```
concepts/
  001-slug/
    plan.md            # the plan (Adam + Meta draft it)
    feedback-meta.md   # Meta's feedback (Meta authors, Luma commits)
    feedback-claude.md # Claude's feedback (Claude authors, Luma commits)
    feedback-gemini.md # Gemini's feedback (Gemini authors, Luma commits)
    final.md           # Adam + Luma's synthesis (maintainer-only edits)
    manifest.json      # transaction log (maintainer-only edits)
_template/             # blank copies of the above; Luma copies these per concept
```
