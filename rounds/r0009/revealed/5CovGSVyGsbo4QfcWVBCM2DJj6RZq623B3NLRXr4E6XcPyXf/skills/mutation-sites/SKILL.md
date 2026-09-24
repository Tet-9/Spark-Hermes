---
name: mutation-sites
description: How to find a small injected edit by disagreement with the docstring, a sibling, or the surviving tests.
---

# Find the edit by disagreement

Read this after the repro, before you change a line.

The bug is a small change to working source, not a missing feature. The function still exists. One expression, one argument order, one branch, or one XML update is wrong.

## What to compare

- The docstring and the return line. If they disagree, believe the docstring and the tests that still import the symbol.
- A sibling function in the same file that does the paired job (before/after, top/bottom, get/set, parse/generate). The broken one is the one that no longer matches its twin.
- Callers one hop away. A swapped argument shows up as the callee's parameter names not matching the values passed.
- A comment or a constant next to the line (`EMU`, twips, `Pt`, `Emu`). A factor of two, or 635 versus 12700, is a unit mixup, not a new formula to invent.

## Shapes that show up in these trees

- Argument order. The call still type-checks loosely but binds the value to the wrong parameter. Restore the order the callee's signature and the only other call site use.
- A flipped operator or a swapped operand in a parser action. The token is still recognized; the expression tree is built in the wrong order, so generation drops a clause. Match the order used for the sibling clause in the same function.
- A removed branch. A loop or an `if` that used to copy every child now copies one. If a property update deletes siblings, the setter is replacing the parent element. Update the one child and leave the others.
- A getter and a setter that no longer invert each other. Set, then read the same property in `/tmp/repro.py`. If the read is half, double, or zero, the conversion on one side is the bug. Change the side that disagrees with the other properties in that class.

## How many sites

Count symptoms in the issue. Each named symbol or each failing behaviour is its own site until you have checked the function and found it already consistent. Fix the first site, then scan the rest of that file for the same shape. Do not open a second package.

## What not to do

Do not rewrite the function. Do not add a compatibility wrapper. Do not "fix" a neighbouring line you cannot tie to a symptom. If you cannot say which token is wrong, you are not ready to add lines, but you are ready to revert a speculative edit.
