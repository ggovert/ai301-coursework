# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Issue Reference | Candidate PR description or title read against issue context | Cites or links the target issue number (e.g., `#123`, `Closes #123`, `Fixes #123`). | required |
| Template and Policy Standards | Candidate PR description read against repo facts block and PR template | Complies with the repository's stated template and policy asks: fills required template sections without empty placeholders, and includes AI disclosure only if the repo explicitly requires it. | required |
| Plan Fidelity | Unified diff read against the plan's scope, test plan, and deviation notes | Diff implements the planned changes without silent additions or unapproved scope expansion; any omission or design shift is explicitly documented under deviations and disclosed in the PR. | required |
| Clean Diff | Unified diff hunks and file modifications | Diff is focused and free of debugging debris (stray print/console statements), commented-out dead code, temporary artifacts, and unrelated mass reformatting. | required |
| Verification Evidence | Test evidence section read against repo checks and plan | Contains observable evidence verifying the fix (before/after reproduction or test suite runs), with any known limitation or skipped suite honestly explained. | required |
| Description Accuracy | Candidate PR description read against diff | Accurately describes the changes present in the diff without making contradictory or false claims. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

- accept: Every required check grades as pass. The preferred check does not prevent acceptance unless it reveals an unaddressed failure in a required check.
- reject: Any required check grades as fail or unclear.
- unclear treatment: unclear grades count as fail. An unverifiable claim is a failing claim.
- honest shortfall rule: A PR that honestly discloses a planned shortfall, deferred edge case, or known test limitation passes fidelity and verification checks, provided the limitation is documented rather than hidden.
'@