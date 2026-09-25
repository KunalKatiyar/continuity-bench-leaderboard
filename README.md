# Continuity Bench — leaderboard

**Live: https://kunalkatiyar.github.io/continuity-bench-leaderboard/**

Static leaderboard for [continuity-bench](https://github.com/KunalKatiyar/continuity-bench): how well do models
detect continuity errors in novel-length fiction, and what does each detection cost?

**This repo is generated output.** Nothing here is edited by hand. The site, the
harness and the corpus builder live in the benchmark repo; this repo exists so the
leaderboard can be hosted and shared on its own.

## Hosting

No build step, no dependencies — it is one self-contained `index.html`.

- **GitHub Pages:** Settings → Pages → deploy from branch `main`, folder `/`. The
  `.nojekyll` file is already present so Pages serves the file as-is.
- **Anything else:** serve the directory, or open `index.html` from disk.

## Regenerating

From the benchmark repo:

```bash
./publish_leaderboard.sh ../continuity-bench-leaderboard
```

That re-renders `index.html` and refreshes `data/results/`, which holds one JSON per
run — every number on the page, plus per-novel and per-rule breakdowns that the page
does not show.

## Reading it

The headline metric is **J = recall − false-positive rate**, not F1. On this corpus
every injected passage is paired with the same passage unedited, so flagging everything
scores F1 0.667 while discriminating nothing — a real model has scored exactly that.
J is 0 for any such strategy and 1 for a perfect one.

Integrity checks are listed separately from contenders. They are not models; they are
the heuristics and diagnostics that decide whether the leaderboard is worth reading.
