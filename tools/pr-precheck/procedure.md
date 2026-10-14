# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. **Read Issue Context and PR Template**:
   - In Live Mode, read `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and the target issue description.
   - In Eval Mode, read the package header, repo-facts, and issue context block.
   - Purpose: Establish the baseline requirements and the bug being fixed before viewing any implementation.
2. **Read Implementation Plan**:
   - Read `plan.md` (or the plan block in the package), specifically noting the planned files, technical approach, and any recorded `## Deviations`.
3. **Read Git Diff**:
   - Read the committed changes (`git diff main...HEAD` in live mode, or the diff section in eval packages).
   - Note which files are modified, added, or deleted, and inspect lines for debugging debris or unrelated refactors.
4. **Read Test Evidence**:
   - Read `test_evidence.md` (or the package test block), noting the before/after repro outputs and the `make test-unit`, `make lint`, and `make typecheck` results.
5. **Read Candidate PR Title and Description**:
   - Read `pr_draft.md` (or package PR draft block). Note the issue link, changes listed, testing checkmarks, demo note, and AI disclosure in Notes for Reviewers.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

Gather facts across the four core dimensions:
1. **Standards & Template**:
   - Check if `Closes #<id>` appears in the issue section.
   - Check each template header (`## Summary`, `## Issue`, `## Changes`, `## Testing`, `## Screenshots / Demo`, `## Notes for Reviewers`) for substantive text vs. placeholder text.
   - Find the explicit AI disclosure sentence under `Notes for Reviewers`.
2. **Plan vs. Diff Pairing (Silent Drift)**:
   - Compare the list of modified files in the diff with the files named in the plan.
   - Check whether any diff change not in the original plan is justified in `plan.md` under `## Deviations`.
   - Check whether any change promised in the plan was silently omitted from the diff.
3. **Diff Hygiene (Unreviewable)**:
   - Scan diff hunks for console logs, debug prints, stray commented-out code, temporary test files, or mass reformatting.
4. **Test Evidence (Not Tested)**:
   - Locate the before-and-after reproduction run logs. Verify that the before run demonstrates the failure and the after run shows the fix working.
   - Locate the make check outputs. Verify unit tests, linting, and typechecks were actually run.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Execute checks sequentially in rubric order:
   - `Issue Linkage`
   - `Template Completeness`
   - `AI Disclosure`
   - `Plan Fidelity`
   - `Clean Diff`
   - `Verification Execution`
   - `Repro Evidence`
   - `Accurate Changes`
2. Grade each check as `pass`, `fail`, or `unclear`:
   - Quote the deciding text, file name, or line as evidence.
   - If evidence for a check is absent, grade it `fail` citing missing evidence.
   - If an honest deviation or disclosed test failure is present, evaluate whether it was explicitly disclosed in both the plan and the PR description. If honestly disclosed, pass `Plan Fidelity`.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Tally check grades:
   - If all `required` checks grade as `pass`, the final verdict is `accept`.
   - If any `required` check grades as `fail` or `unclear`, the final verdict is `reject`.
2. Format the output:
   - Print a readable summary listing each check, its grade, and its deciding evidence.
   - If rejecting, highlight the first failing required check and state the remediation action.
   - In Live Mode, append any voice-guide violations found in the PR title or description.
   - Conclude with the required JSON block containing `item`, `checks`, and `verdict`.
