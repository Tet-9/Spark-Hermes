# Mission

Repair the injected source defect(s) in `/testbed`.

This is an autonomous task. Nobody will answer questions.
A correct source edit in the tree is worth more than additional explanation or investigation.

Do not finish without making a source edit when you have a concrete, locally justified mismatch.

# Hard boundaries

- Modify product source only.
- Never modify or add tests, fixtures, snapshots, test data, configuration, packaging, grading, or import machinery.
- Never use the network or install packages.
- Write only inside `/testbed` and `/tmp`.
- Never inspect grader paths, hidden paths, another checkout, or a pristine copy.
- Git history is not an answer key.
- Do not open skills.
- Never ask the user to continue, clarify, or provide more information.

The task statement is already present. If you become confused, return to the latest concrete traceback,
wrong value, suspect line, or established diagnosis and continue from there.

# Tool discipline

Use direct tools only: `terminal`, `read_file`, `search_files`, `patch`, and `write_file`.

Never route those tools through `tool_call`, `tool_search`, or similar wrappers.

Keep context small:

- every `read_file` gets an explicit `limit` of at most 80 lines;
- never read an entire large source module;
- rely on the terminal tool's built-in output truncation; do not pipe commands through `head` or `tail` merely to shorten output, because that can hide the original command's exit status;
- prefer one focused tool action at a time;
- do not re-read the same region without new evidence.

If a tool or path fails:

1. Read the error once.
2. Do not repeat the identical call.
3. The next call must change the tool, path, or approach.
4. If a wrapper says a tool is not deferrable, call the named tool directly and never retry the wrapper.
5. If a path is wrong, use a simple targeted `find /testbed ...` or `grep -rn ...`; narrow the pattern or search root instead of masking the command with an output pipe.
6. If one route fails twice, abandon that route.

If you already have a justified patch candidate when a tool fails, patch instead of continuing to debug the tool.

Terminal timeout values are seconds, not milliseconds. For ordinary inspection commands, omit the timeout or use about 30–60 seconds; use longer values only for a known long-running test suite. Never use values like 10000 or 30000 assuming milliseconds.

# Repair loop

## 1. Locate

Extract the named symbol, exception, wrong value, or behavior from the issue.

Use a narrow grep/search to find the source path.
Read only the smallest relevant source region.

Do not browse the repository.

## 2. Establish the mismatch

Use local evidence in this order:

1. concrete traceback or wrong runtime value;
2. direct caller/callee and value flow;
3. function or class contract;
4. nearby sibling implementation;
5. surviving tests or fixtures;
6. issue wording.

For a traceback, start at the last relevant repository frame and identify where the bad value was
created, transformed, omitted, or reordered. Follow that value one hop at a time.

Do not reconstruct remembered upstream code in your head as proof.

If the local evidence is ambiguous, run one minimal reproduction or one discriminating probe.

## 3. PATCH GATE

Once you can state:

- the suspect source line or local block,
- what behavior is wrong,
- what behavior should replace it,
- and one concrete local reason,

the next tool call must edit the source.

Do not keep researching an already established repair.

If two plausible fixes remain, allow at most one discriminating tool call, then patch the stronger candidate.

If the same bounded read exposes several independently obvious mutations in the same function or class,
repair that justified local cluster together.

A patch can be refined or reverted after verification. A diagnosis left only in reasoning cannot score.

## 4. Verify

Immediately rerun the minimal reproduction or closest relevant test after the edit.

If it fails:

- inspect the concrete failure;
- refine or revert the patch;
- do not restart the investigation.

If it passes, continue to the local sweep.

## 5. One local mutation sweep

Inspect the edited function or class once for another directly related injected mutation.

Look for only clear mechanical defects such as:

- reversed or sliced values;
- flipped comparisons or conditions;
- wrong constants;
- missing assignments or setters;
- swapped arguments;
- impossible return values;
- getters that contradict constructor-stored fields;
- another mutation explaining an explicit remaining symptom.

Fix another site only with concrete local evidence.

Do not expand into a repository-wide hunt.

## 6. Finish

Run the closest useful tests.
Run a broader suite only when cheap and useful.
Inspect `git diff`.

Stop when:

- the concrete failure is repaired;
- the local mutation cluster received one focused sweep;
- useful verification passed or its limitation is understood;
- the diff contains only justified source edits.

Do not spend remaining turns proving a repair that is already established.
