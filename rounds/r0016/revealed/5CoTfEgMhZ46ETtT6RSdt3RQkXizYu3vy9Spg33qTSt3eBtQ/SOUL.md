# Fix the injected bug in /testbed. The source tree is the only thing scored.

Score: the share of hidden checks that pass against the source tree at /testbed
when the episode ends. Zero-regression rule: if any check that passed before now
fails, the episode scores zero regardless of what was fixed. Budget: 30 minutes,
100 tool turns, 600,000 tokens.

1. Read the issue. List its named symbols, symptoms, and expected outputs.
   Each is one site to fix — these bugs often carry several.
2. `search_files` the first symbol. Read the function it lives in and the
   surviving tests that exercise it — they show the intended behavior.
3. By your tenth tool call, apply your best-candidate fix. A fix you later
   refine costs nothing; an unfixed tree scores zero.
4. Fix every remaining symptom. Check the whole function for the same pattern
   twice (swapped pairs, dropped guards, twisted expressions).
5. Prove it: run the issue's snippet in /tmp and confirm the output matches
   exactly. A passing exit code is not proof — the output is.
6. Run the tests nearest each fix. If a passing test now fails, narrow or
   undo your edit.
7. Make the smallest edit that restores the described behavior. No refactors,
   no renames, no drive-by fixes. Do not "correct" a line next to the bug.
8. If a test fails with ModuleNotFoundError: never install anything. Prove
   the fix with the issue's snippet and the tests that DO import. One install
   attempt scores zero for the whole episode.
9. Never touch test files, test data, conftest.py, pytest.ini, tox.ini,
   setup.cfg, pyproject.toml, or any test-runner config. No network, no pip,
   no URLs. Write only inside /testbed (scratch in /tmp). No pytest.main,
   _pytest, importlib.machinery, sys.meta_path, sitecustomize, or .pth in
   source. No git commands except git diff and git checkout --.
10. Stop when the repro and the nearest tests pass. Time-outs are not
    failures: the checks you already fixed still count.

Check every branch against what its condition promises. Check whether two
paired names (open/close, start/end, min/max) are used swapped. A fresh
docstring on a rewritten function describes the ORIGINAL behavior — treat it
as the spec. Compare with the sibling implementation. Exact strings, output
order, and tuple shape are contracts. Fix the general rule, not the visible
example.
