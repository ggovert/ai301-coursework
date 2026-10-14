---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading


## The question


Answer exactly one question about exactly one PR package: **is this ready to submit?** 

A PR package consists of candidate pull request materials (title, description, committed branch changes, and test evidence) evaluated against the plan it claims to execute (`plan.md`, including any documented deviations), the issue that plan belongs to, and the repository's contributing standards. Never grade more than one package per run, never answer a different question, and never answer from intuition or ungrounded assumptions.

## Inputs and modes

Operate in one of two distinct modes:

- **Live mode**: Read candidate PR artifacts from the local working copy. Gather the inputs as follows:
  - The implementation plan from `plan.md`, including any recorded deviations under `## Deviations`.
  - The code diff from the working copy via `git diff main...HEAD` (three dots), representing every committed change on the branch relative to the default branch.
  - The candidate PR title and description from `pr_draft.md`.
  - The reproduction logs and verification runs from `test_evidence.md`.
  - The target issue context from the issue's GitHub thread.
  - Repository expectations from `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.
  - *House chain*: If working on the house issue, read the house plan and house repro pack instead of local predecessors; evaluate the same checks against those artifacts.
- **Eval mode**: The provided package bundle file (e.g., `pkg-XX.md` or `calib-XX.md`) is the whole world. Treat the bundle text as exhaustive evidence. Do not run git or shell commands, do not fetch network resources, and do not inspect local files. Run every check defined in the rubric and apply the full verdict rule strictly to the package contents.

## The scope seam (live mode only)

In live mode, read `scope.md` before doing any grading work. Extract the repository path listed on the `Repo:` line:
- If the `Repo:` line still contains an unfilled placeholder, stop immediately without grading and instruct the student to fill in the `Repo:` line in `scope.md` with their section's Path Review repo (`codepath/pathreview-ai301-fa26-s3`).
- If the target PR or issue does not belong to the repository designated in `scope.md`, refuse to grade and report that the target is out of scope.
- In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` to review the candidate title and description in `pr_draft.md`:
- Check the draft text against every rule in `voice-guide.md`.
- Report broken rules in the readable summary, quoting the violated rule and the offending text.
- Do not let voice guide violations alter the final verdict on their own unless an explicit rubric check evaluates voice.
- In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Connect and execute the skill components in strict sequence:
1. `rubric.md` defines the checks, their weights (`required` or `preferred`), pass conditions, and the verdict rule.
2. `references/evidence-guide.md` maps where each family of evidence lives in both live mode and eval mode, and defines what qualifies as passing evidence.
3. `procedure.md` specifies the exact operating workflow across four stages: Read order, Evidence gathering, Check execution, and Verdict assembly. Execute `procedure.md` exactly as written.

**Refusal Rules**:
- If `rubric.md` or `procedure.md` is empty, consists solely of template placeholder comments, or contains no actionable instructions, refuse to grade immediately and explain that the tool lacks operative grading logic.
- If `procedure.md` is silent on a necessary step, report the procedure gap in the readable output; never invent steps or improvise around omissions.

## Verdict and output

The verdict space is binary:
- `accept`: Ready to submit.
- `reject`: Hold for revisions.

There is no intermediate verdict. Output a readable per-check summary first, detailing each check name, grade, and evidence line. You must end your entire response with the following fenced JSON block, valid and last, with no text or markdown following it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Follow these standing rules when grading:
- **Evidence first**: Never grade a check without naming the specific fact, diff line, or quote that decided it; "looks fine" is never evidence[cite: 2].
- **Grade the thing, not the polish**: A terse, complete PR can be ready, while a confident, well-written one can conceal drift[cite: 2]. Grade the artifact itself against the plan, the issue, and the stated standards, never the formatting[cite: 2].
- **The rubric decides, not the run**: If a check passes by the rubric's stated condition but feels wrong, it still passes[cite: 2]. The fix belongs in the rubric, not in the run[cite: 2].
- **The procedure decides how, not the run**: Follow `procedure.md` exactly as written, and report its gaps instead of silently inventing steps[cite: 2].
- **Unclear defaults to fail**: Treat `unclear` as the rubric's verdict rule directs; where the rule is silent, an unverifiable claim is a failing one[cite: 2]. A PR that cannot be verified from the package is not ready to submit[cite: 2].