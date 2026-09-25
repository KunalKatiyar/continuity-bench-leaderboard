# Continuity Bench — leaderboard

**Live: https://kunalkatiyar.github.io/continuity-bench-leaderboard/**

How well do models spot continuity errors in novel-length fiction, and what does each
catch cost? This repo is just the scoreboard. The corpus builder, the evaluation harness
and the Jev pipeline live in
[continuity-bench](https://github.com/KunalKatiyar/continuity-bench).

Nothing here is hand-edited. It is one self-contained `index.html` plus the raw per-run
JSON, regenerated from the benchmark repo with:

```bash
./publish_leaderboard.sh ../continuity-bench-leaderboard
```

## Hosting it

No build step, no dependencies. GitHub Pages serves it from the branch root, and
`.nojekyll` is already there so the file goes out untouched. Anywhere else, serve the
directory or just open `index.html`.

## Reading it

The headline number is **J = recall − false-positive rate**, not F1. Every injected
passage in this corpus is paired with the same passage left alone, so flagging everything
scores F1 0.667 while separating nothing. An 8B model has scored exactly that. J is 0 for
any such strategy and 1 for a perfect one.

Each run carries a 95% interval, and two cases that look alike get marked differently: an
interval tight around zero means the model genuinely doesn't discriminate, while a wide
one means the run was too small to tell.

Integrity checks are listed apart from the contenders. They aren't models. They are the
heuristics and diagnostics that decide whether the board is worth reading at all, and one
of them tops +0.699 by exploiting the release format rather than reading the text.

`data/results/` holds one JSON per run, with the per-novel and per-rule breakdowns the
page leaves out.
