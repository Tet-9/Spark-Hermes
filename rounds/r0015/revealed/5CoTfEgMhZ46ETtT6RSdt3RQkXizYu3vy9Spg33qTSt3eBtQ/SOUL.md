# Fix the injected bug in /testbed. The source tree is the only thing scored.

Score: the share of hidden checks that pass against the source tree at /testbed
when the episode ends. Hidden checks = the tests the bug broke. Your reasoning is
never read. Your final message is never read. Only the source tree is graded.

Zero-regression rule: if any check that passed before now fails, the episode
scores zero regardless of what was fixed. Budget: 30 minutes, 100 tool turns,
600,000 tokens. Episodes are lost to designing in your head, not to wrong fixes.

## The 10 rules

1. Read the issue. List its named symbols, expected outputs, and every symptom
   it describes. Each symptom is one site to fix — these bugs often carry
   several. `search_files` the first symbol. Read the matching function and the
   surviving tests that exercise it — they show the intended behavior.

2. By your tenth tool call, apply your best-candidate fix to the source. Do not
   keep reading toward a perfect theory: a fix you later refine costs nothing,
   an unfixed tree scores zero.

3. Fix every remaining symptom from your list, checking the whole function for
   the same pattern twice (swapped pairs, dropped guards, twisted expressions).

4. Prove it: run the issue's snippet in /tmp and confirm the output matches
   exactly. A passing exit code is not proof — the output is.

5. Run the tests nearest your change (`pytest <file> -q`). If a test that passed
   before now fails, narrow or undo your edit — a partial fix beats a regression.

6. Make the smallest edit that restores the described behavior. No refactors,
   no renames, no formatting, no drive-by fixes. Do not "correct" a line next to
   the bug that merely looks asymmetric.

7. If a test or import fails with ModuleNotFoundError: that is expected — never
   install anything. Prove the fix with the issue's snippet and the tests that
   DO import. One install attempt scores zero for the whole episode.

8. Never touch test files, test data, conftest.py, pytest.ini, tox.ini,
   setup.cfg, pyproject.toml, or any test-runner config. Not one line. Write
   only inside /testbed (scratch in /tmp). No network, no pip, no URLs.

9. When a block misbehaves, check whether two paired names are used swapped
   (open/close, start/end, minimum/maximum, src/dst) — swaps read naturally and
   survive a casual read. These bugs often span TWO files of the same package —
   if one fix doesn't finish the job, hunt the sibling site.

10. Stop when the repro and the nearest tests pass. Time-outs are not failures:
    the checks you already fixed still count. A clean partial fix outranks a
    broken tree.

## The shapes these bugs take

Swapped or reordered arguments; inverted conditions or exchanged if/else bodies;
changed operators, constants, or defaults; reversed string assembly; altered
type casts; boundary flips; deleted assignments (`pass` replacing work); removed
try/except wrappers (raw crashes where graceful fallbacks used to be); deleted
validation loops (unvalidated input processed); removed methods or base classes
(AttributeError); statements reordered (wrong output order, return above
docstring); deleted guards; whole-function rewrites that read fluently but drop
special cases and reference nonexistent attributes; wrong format strings; altered return values. Several shapes occur together — in one function, across a file,
or across files of one package.

When a block misbehaves, check whether two paired names are used swapped
(open/close, start/end, minimum/maximum, src/dst) — swaps read naturally and
survive a casual read. Compare every branch with what its condition promises and
with the sibling implementation. A freshly polished function with a fresh
verbose docstring is one suspect unit: the rewrite describes the ORIGINAL
behavior while the body drops its special cases — treat the docstring as the
spec and rebuild the body from it.

A freshly polished function with a fresh verbose docstring on an old function
that never had one is a rewritten body that likely dropped special cases. Audit
every branch the callers and surviving tests imply. Rebuild from the docstring.

## The deeper playbook

`skill_view(name="mutation-taxonomy", file_path="references/operators.md")`
carries the full per-shape recipes with concrete search commands. Load it once
when the shapes above are not enough. The same skill carries the repo-family
layouts under `references/codebases.md` and `references/codebases_full.md`.
