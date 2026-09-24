# Restore the broken behaviour without breaking the rest

`/testbed` is one Python library with a few small source edits. Credit is the share of the tests those edits broke that pass again. If any test that already passed now fails, the episode scores zero. A partial fix that leaves the suite green is worth credit. A regression is worth less than doing nothing.

## Budget

You have a token budget. The whole transcript is resent on every step, so a large tool result is paid for again and again. Plan on about thirty useful steps. Read slices, not whole files. Run tests quietly. Open one skill when you need it, then do not open the others.

## Loop

1. Read the issue once. List every symptom and every named symbol. Several symptoms usually mean several independent edit sites, often in one file.
2. `ls /testbed` and open `tree-layout` once, for this repository only. Take the test command and the module that owns the named symbol. Do not browse.
3. Reproduce before editing. If the issue has a snippet, save it under `/tmp/repro.py` and run it with the project on `PYTHONPATH` (`cd /testbed`). The traceback is the first site. If there is no snippet, call the named function with the values the issue states.
4. Open `mutation-sites`. Compare the failing line with its docstring, its type hints, a sibling that does the same job, and a caller. The injected edit is a small disagreement: swapped arguments, a flipped operator, a dropped branch, a setter that replaces an element instead of updating one attribute, a unit conversion off by a constant factor.
5. Edit by step ten even if you are unsure. An episode that only reads scores zero. Change the smallest span you can justify. No rename, no reformat, no drive-by cleanup.
6. Re-read only the file you changed and match each symptom to a site. If one symptom is still unexplained, fix that site next.
7. Open `green-suite`. Run the test file that covers the module, then a slightly wider quiet run if the budget allows. A new failure means narrow the edit or `git checkout -- <path>` before you stop.

## Undo

History is one commit and no remote. It does not explain the bug. `git diff` is the list of what you changed. `git checkout -- <path>` restores a file. Read the diff before you stop and put back anything you did not mean to change.

## These end the task at zero

- No network. Do not install, fetch, or clone. One outbound attempt ends the episode.
- Do not search the machine for another copy of the library or another Python. Import the package from `/testbed`.
- Do not touch tests or test configuration: no file under a test directory, no `conftest.py`, no `pytest.ini`, no `tox.ini`, no `setup.cfg`, no pytest section of `pyproject.toml`, no fixture or golden file.
- Do not run a flag that rewrites expected output.
- Write only under `/testbed` and `/tmp`. Do not inspect how grading works.
- Do not import the test runner from project source, reload modules to hide a change, or patch import machinery.
- Do not fill the disk.

## Order of outcomes

1. Every injected site fixed, and nothing that passed before now fails.
2. Some sites fixed, and nothing that passed before now fails.
3. The tree exactly as you found it.

Never leave the repository more broken than you found it.
