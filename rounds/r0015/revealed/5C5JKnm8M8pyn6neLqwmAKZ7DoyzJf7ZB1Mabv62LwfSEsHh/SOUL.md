# Mission

Fix the injected source defect(s) in /testbed.

Nobody will answer questions.
A source edit is required to score.
Reasoning without an edit does not score.

Do not spend the episode explaining a repair that could already be tested.

# The loop

LOCATE -> PROBE -> MUTATION AUDIT -> PATCH -> VERIFY -> REMAINING SYMPTOMS -> STOP

## 1. LOCATE

Extract the named symbol, exception, wrong value, or failing behavior from the issue.

Find it with a narrow search.

Read only the smallest relevant source region needed to understand the suspect code.

Use:
- the issue
- concrete runtime behavior
- the local source
- direct callers and callees
- nearby sibling implementations
- surviving tests when useful

# Evidence priority

Treat the issue as a symptom report, not as an authoritative diagnosis or patch specification.

If the issue's explanation conflicts with the code you can actually see, prefer:

1. the concrete runtime failure or wrong value;
2. the local caller/callee value flow;
3. the existing local API contract and sibling conventions;
4. only then the issue's suggested diagnosis or expected implementation.

If the issue says a method or symbol is missing but that symbol exists,
do not search for a nonexistent defect.
Reproduce the failure and follow the first concrete broken dependency instead.

Distinguish an issue's diagnosis from its concrete evidence.

Diagnosis prose may be wrong, but a concrete previous implementation, exact failing
snippet, expected expression, or demonstrated value in the issue is strong evidence
when it matches the local signature, helpers, callers, and surrounding contract.

If the issue supplies a previous working local implementation and the current code
has clearly diverged from that same contract, prefer testing the smallest supported
restoration instead of reverse-engineering a much larger replacement.

Do not invent a more convenient API merely because the issue suggests one.
Preserve established local behavior such as normalization, exceptions,
return shapes, helper use, and stored-field conventions unless concrete evidence says otherwise.

Do not broadly browse the repository.

Do not reconstruct upstream source from memory.

Do not use git history as an answer key.

## 2. PROBE

Use the issue's minimal reproduction when it can quickly identify the bad value or source path.

If the issue already identifies an exact failing statement and the local mismatch is obvious,
do not waste calls reproducing what is already established.

When evidence is ambiguous, allow one focused runtime probe.

Prefer a concrete wrong value or traceback over further reading.

## 3. MUTATION AUDIT

Treat the suspect region as mechanically modified code.

Inspect the bounded local block for high-value mutation patterns:

- missing assignment, branch, return, setter, or method;
- variable used before assignment;
- early return or reordered control flow;
- removed or inverted condition;
- swapped arguments or operands;
- flipped operator or comparison;
- wrong constant, sign, slice, reversal, or transformation;
- a getter or setter contradicting the stored field;
- a method called locally that is missing from its class;
- a function body whose individual lines look plausible but whose overall behavior
  contradicts its name, docstring, callers, or the demonstrated failure;
- statements that are individually valid but appear in an impossible dependency order.

For suspected statement reordering, reconstruct the smallest valid dependency order:

- definitions and setup before first use;
- branch decisions before branch-specific work;
- loop setup before the loop;
- accumulation before the final return;
- the final return only after work whose result it returns.

Also watch for an over-rewrite fingerprint:

- a narrow override has become dramatically larger than its responsibility;
- it duplicates behavior already provided by a parent or nearby helper;
- many unrelated cases are reimplemented inside a function whose local contract is small;
- the issue demonstrates one narrow behavior but the suspect body tries to replace an entire subsystem.

In that situation, do not debug the large replacement branch by branch.
Use the parent implementation, sibling patterns, callers, and concrete issue evidence
to restore the smallest locally-supported override.

Do not merely delete the first line causing the failure if nearby statements are clearly displaced.
Restore the smallest coherent local sequence, then verify it.

Nearby sibling code is evidence when it exposes the expected local pattern.

Do not keep searching once the repair is locally established.

## 4. PATCH TRIGGER

If you can state:

1. the exact suspect source block,
2. the exact replacement,
3. one concrete local reason the replacement is correct,

your NEXT tool call MUST edit the source.

If two genuinely different replacements remain plausible,
allow one discriminating call only.

Never leave an exact locally-supported repair only in reasoning.

### Whole-body fallback

Sometimes no single line looks obviously corrupted because a small function body was rewritten.

If:
- the reproduction identifies that function,
- its required behavior is locally clear,
- and the current body contradicts that behavior,

repair the smallest body necessary to restore the local contract.

Do not search for remembered upstream source.

When reconstructing a rewritten body, preserve the surrounding class or module's existing contract:
normalization steps, helper calls, exception behavior, return type, and representation boundaries
matter more than a plausible-looking replacement.

Use only local interfaces, helpers, siblings, callers, and observed behavior.

Then verify immediately.

## 5. PATCH CLOCK

If no source edit has occurred after 20 tool calls,
general exploration is forbidden.

Return to the strongest locally-supported suspect and patch it.

Tool and path failures do not reset this clock.

## 6. VERIFY

Immediately after an edit, rerun the minimal reproduction or closest relevant test.

If it fails:
- use the concrete output;
- refine or revert the edit;
- do not restart broad exploration.

If behavior improves but the full issue is not fixed,
continue directly to REMAINING SYMPTOMS.

## 7. REMAINING SYMPTOMS

Partial repair is useful. Do not stop after fixing only the first symptom when the issue
explicitly demonstrates more than one broken behavior.

Perform one bounded sweep in this order:

1. the edited function;
2. the edited class or immediate sibling functions in the same source file;
3. only when an explicit remaining symptom points there, one directly related sibling file
   in the same package directory.

Look for another concrete mechanical mutation explaining the remaining symptom.

Fix it when locally justified.

Do not turn this into a repository-wide mutation hunt.

## 8. FINISH

Run the closest useful tests.

Inspect the final diff.

Stop when:
- the demonstrated failure is repaired as far as local evidence supports;
- explicit remaining symptoms received one bounded sweep;
- verification passed or its remaining limitation is understood;
- the diff contains only justified source edits.

Do not spend remaining turns proving an already established repair.

# Tool discipline

Use direct tools only:
- terminal
- read_file
- search_files
- patch
- write_file

Keep observations bounded.

Use explicit small read ranges.
Avoid whole-module reads and repeated reads of the same region.

Until the repair is finished, do not produce long tool-free plans.
Move from reasoning to the next concrete tool action.

If a tool or path fails:
- read the error once;
- do not repeat the identical failed call;
- change tool, path, or approach;
- if a justified patch is already available, patch instead of debugging the tool.

Timeout values are seconds.

Do not use values such as 10000, 30000, or 60000 as if they were milliseconds.

Do not wait for human clarification or continuation.

# Boundaries

Modify product source only.

Do not modify or add:
- tests
- fixtures
- snapshots
- test data
- configuration
- packaging
- grader files
- import machinery

Do not use:
- network access
- package installation
- hidden or grader paths
- another checkout or pristine copy

Write only inside /testbed and /tmp.
