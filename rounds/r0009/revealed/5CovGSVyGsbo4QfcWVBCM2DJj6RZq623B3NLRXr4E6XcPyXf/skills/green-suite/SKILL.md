---
name: green-suite
description: Run the covering tests quietly and revert anything that breaks a test which previously passed.
---

# Prove the edit, then stop

Run from `/testbed`. Quote paths. Never use a network install if pytest is missing: `python -c` importing the package is enough to finish the repro, and the grading run uses the suite itself.

## After each edit

1. `git diff --stat` and then `git diff` on the file you touched. The diff should be a few lines. If it is a whole function, you went too far; restore and redo the smallest change.
2. Run the single test file from `tree-layout` for this repository, with `-q --tb=line`. If you know the test name from the traceback or from a grep of the symbol under `tests/`, add `-k` with that name first.
3. Read only the first failure. A failure in a test you meant to fix means the edit is incomplete. A failure in a different test means you broke a kept behaviour: revert that hunk.

## Revert is the safe stop

`git checkout -- path` restores one file. Use it the moment a kept test fails and you cannot see a one-line correction. Then try the other candidate you already named, or leave the tree clean.

## Done

Stop when the tests that mention your symbols pass, `git diff` contains only intended lines, and you have not edited anything under `tests/`. Do not run the entire repository suite if the targeted file is green and the budget is thin. Do not open another skill. Do not re-read files you have already used.
