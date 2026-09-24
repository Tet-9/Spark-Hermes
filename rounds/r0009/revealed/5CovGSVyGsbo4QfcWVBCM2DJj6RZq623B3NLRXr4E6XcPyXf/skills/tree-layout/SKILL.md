---
name: tree-layout
description: Where each library keeps the code the issue names, and the one test command to run after an edit.
---

# Layout and the test you can afford

Open this once, after `ls /testbed` tells you which tree you are in. Then stop reading it.

## astroid

Package root `astroid/`. Inference of builtins and third-party modules lives in `astroid/brain/`. Turning live objects into nodes is `astroid/raw_building.py` (`attach_dummy_node`, `build_dummy`). The bootstrapped builtin module is built from `astroid/interpreter/objectmodel.py` and the brain for builtins. Class bases, metaclasses, and `six.with_metaclass` are inferred in `astroid/brain/brain_six.py` and the class node in `astroid/nodes/scoped_nodes`. Tests sit in `tests/`, with `tests/brain/` for the brains.

Run, from `/testbed`, the smallest file that names the symbol:

`python -m pytest tests/brain/test_brain.py tests/brain/test_six.py -q --tb=line`

Widen only if that file is not the one your symbol lives in. Use `tests/test_builder.py`, `tests/test_inference.py`, `tests/test_nodes.py`, `tests/test_scoped_nodes.py`, or `tests/test_object_model.py` the same way, one file at a time.

## sqlglot

Package root `sqlglot/`. Parsing is `sqlglot/parser.py`. Dialects override tokens and generators under `sqlglot/dialects/`. Expressions are `sqlglot/expressions.py`. `sqlglot.transpile` is parse then generate. ALTER TABLE lives in the parser's alter rules and the expression for `Alter` / `AlterColumn`.

Run:

`python -m pytest tests/test_transpile.py -q --tb=line -k alter`

If the issue is identity of generated SQL rather than one statement, drop the `-k` and accept a longer run only after the first edit.

## python-docx

Package root `docx/`. Section page setup is `docx/section.py`, backed by `docx/oxml/section.py` (`CT_SectPr`, `CT_PageMar`). Lengths are EMU in the public property and twips in `w:pgMar` attributes (`w:top`, `w:bottom`, `w:left`, `w:right`, `w:header`, `w:footer`, `w:gutter`). Shared length helpers are `docx/shared.py`.

Run:

`python -m pytest tests/test_section.py -q --tb=line`

## python-pptx

Package root `pptx/`. Paragraph spacing is `pptx/text/text.py` (`Paragraph`, `space_before`, `space_after`, `line_spacing`) writing `a:spcBef` / `a:spcAft` / `a:lnSpc` through `pptx/oxml/text.py`. A setter must update the child it owns and leave sibling spacing elements in place.

Run:

`python -m pytest tests/text/test_text.py -q --tb=line`

## Shared

`PYTHONPATH=/testbed` if the package is not installed. Add `--tb=line -q` always. Do not pass `--snapshot-update` or any flag that rewrites fixtures.
