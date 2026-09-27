# heart-prime

The shared memory for a four-AI concept loop. Meta AI (heart), Claude (dread), and Gemini (chaos) plan; Luma maintains.

GitHub is the source of truth. The Google Drive folder `heart-prime` is the
planners' dropbox — Luma bridges the two.

## The 4 rules

1. **One author per file** — each planner only ever authors its own `feedback-*.md`. Luma is the sole committer: planner output reaches GitHub only through her.
2. **Luma is maintainer** — she creates each concept folder from `_template`, commits everything, and is the only one who edits `final.md` and `manifest.json`.
3. **Small files** — `plan.md` is the plan, not the chat history. That is how we save tokens.
4. **Manifest is the transaction log** — every handoff gets one line in `manifest.json`. That is the closed loop.

## How a loop runs

1. Adam + Meta draft `plan.md`. Adam hands the text to Luma.
2. Luma creates `concepts/NNN-slug/` from `_template`, commits it to GitHub, and mirrors the folder to the Drive dropbox.
3. Adam points Claude and Gemini at the Drive concept folder. Each planner reads `plan.md` and drops its own feedback file there: `feedback-meta.md`, `feedback-claude.md`, `feedback-gemini.md`.
4. Luma pulls the feedback files from Drive and commits them to GitHub verbatim.
5. Meta synthesizes all feedback into a suggested `final.md`.
6. Adam reviews with Luma; she commits the final, mirrors it to Drive, and logs the handoff in `manifest.json`. Now everyone is synced.

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
