# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

### Where it lives
- **Eval bundle**:
  - Implementation plan and boundaries: `## Plan Context` or `## Plan` (specifically the scope pair: what will change vs. what will not change, and any `## Deviations`).
  - Actual changes: `## Diff` (or unified diff block) and commit list.
  - Claimed changes: `## Description` (specifically under the `Changes` section).
- **Live mode**:
  - Implementation plan: `plan.md` in your repository root, including any updates under `## Deviations`.
  - Actual changes: `git diff main...HEAD` (all committed changes on the branch relative to `main`).
  - Claimed changes: `pr_draft.md` under the `## Changes` header.

### What good looks like
- Every file and function modified in the diff falls inside the boundary stated in the plan's scope pair or is explicitly justified in a `## Deviations` entry.
- The diff does not quietly drop planned tasks, nor does it sneak in unapproved features or refactoring.
- The description's bullet points match the diff exactly: every diff hunk corresponds to a listed change, and no change is claimed that does not exist in the diff.


## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

### Where it lives
- **Eval bundle**:
  - Reproduction and verification: `## Test Evidence` or `## Repro and Tests`.
  - Stated test expectations: `## Plan Context` (under the test plan section).
  - Repo verification checks: `## Repo Facts` (listing mandatory checks like `make test-unit`, `make lint`, `make typecheck`).
- **Live mode**:
  - Test run captures: `test_evidence.md` next to `plan.md`.
  - Draft PR claims: `pr_draft.md` under the `## Testing` section and its checkboxes.

### What good looks like
- Contains paired before-and-after reproduction evidence: the "before" shows the specific error or failure reproducing, and the "after" shows the same command completing cleanly or resolving the defect.
- Terminal outputs for repo checks (`make test-unit`, `make lint`, `make typecheck`) are pasted in full or summarize clean passes.
- A test that cannot pass or run (such as `make test-integration` exiting with "no tests ran") is reported honestly with the terminal output and the reason, rather than omitted or falsely marked as passing.
- The CI checkbox remains unticked prior to opening the PR.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

### Where it lives
- **Eval bundle**:
  - Diff hunks: `## Diff`.
  - Commit history: `## Commits`.
- **Live mode**:
  - Unified diff: `git diff main...HEAD`.
  - Commit log: `git log main..HEAD --oneline`.

### What good looks like
- The diff contains only the minimal changes needed to implement the fix.
- Zero debris: no stray `print()` or `console.log()` debugging lines, no commented-out blocks of dead code, and no temporary files.
- Zero drive-by churn: no mass indentation or reformatting of untouched functions, and no edits to unrelated project files.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

### Where it lives
- **Eval bundle**:
  - Repo expectations: `## Repo Facts` (PR template structure, contributing policy, AI disclosure requirement).
  - Outgoing PR text: `## PR Description` (including title, headers, issue links, and reviewer notes).
  - Thread guidance: `## Issue Context` (maintainer comments and suggestions).
- **Live mode**:
  - Repo requirements: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.
  - Draft PR text: `pr_draft.md`.
  - Thread guidance: The GitHub issue thread.

### What good looks like
- The PR explicitly links the issue using the standard closer keyword: `Closes #<id>`.
- Every section required by the repository's PR template is filled with meaningful, context-specific content; no placeholder text, empty sections, or unedited boilerplate remains.
- The AI-use disclosure is present under `Notes for Reviewers`, stating the tools used and the scope of assistance (or stating none was used).
- If a maintainer gave specific instructions or proposed an approach in the issue thread, the description explicitly acknowledges and addresses it.
