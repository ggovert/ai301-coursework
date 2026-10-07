# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-matches-repro | The plan's stated cause, read against the repro-evidence block (eval) or the student's posted repro comment (live) | The stated cause is consistent with the observed failure in the repro evidence and would explain it. Fail if the diagnosis contradicts the evidence, ignores it, or only restates the symptom. | required |
| cause-not-symptom | The plan's approach and stated cause, read against the repro-evidence block and repo-facts block | The change targets where the bad behavior originates, not just where it surfaces. Fail if the approach patches the visible symptom while the repro evidence points to an upstream cause. | required |
| scope-bounded | The plan's scope statement and files-to-touch list | The plan describes one bounded change and names at least one thing explicitly left out. Fail if it bundles unrelated work, lists no files, or states no limit. | required |
| stranger-can-start | The plan's files-to-touch list and approach, read against the repo-facts block | A person who has never seen the issue could identify what to change and where to start. Pass if the approach names at least one specific file and describes a clear change to make there. Fail only if the approach names no files at all, or is so vague that no starting point can be identified. | required |
| test-plan-observable | The plan's test plan, read against the repro-evidence block's steps and output | The test plan re-runs the repro steps and names a specific observable difference (output, error message, status code) between before and after the fix. Fail if success is stated only as "tests pass" or "it works." | required |
| unknowns-honest | The plan's risks and unknowns section, read against the claims in its diagnosis and approach | The plan does not state unverified claims as settled fact. Pass if uncertain claims are hedged or a risks section exists with any content. Fail only if the plan makes confident causal claims that go beyond what the repro evidence shows, with no acknowledgment of uncertainty anywhere in the plan. | required |
| comment-fits-thread | The plan comment, read against the thread highlights in the issue context (eval) or the live issue thread (live), and against the repo-facts block's stated conventions and contribution policy | The comment responds to what the thread actually contains, follows the repo's stated conventions, and includes any required disclosures such as AI-use. Fail if it ignores maintainer signals, skips required fields, or could be pasted unchanged onto a different issue. | required |

## Verdict rule

Accept if every required check passes. A single required check that fails or is unclear causes a reject. Unclear counts as fail. Preferred checks never change the verdict.