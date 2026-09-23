
# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->


## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `repo-not-archived` | Check the repo-facts block for the archived field | Pass if archived is false | required |
| `maintainer-active` | Check the last 5 default-branch commit dates in the repo-facts block | Pass if at least one commit is within the last 6 months | required |
| `scope-bounded` | Read the issue body for explicit blockers only: is it assigned to a specific person, does it require maintainer-only access, or does it explicitly state it is not suitable for outside contributors | Pass if none of those explicit blockers are present; fail only if the issue body explicitly states it is reserved for maintainers or requires special repository access | required |
| `not-claimed` | Check the issue assignees field, comment thread for any `@zulipbot claim` or similar claim commands, and linked PRs whether open or closed | Pass if assignees is empty AND no linked PRs exist (open or closed) AND no recent claim comment in the thread within 30 days; fail if the issue has a history of repeated claiming and abandonment | required |
| `ai-contribution-allowed` | Check the repo-facts block and CONTRIBUTING.md excerpt for any AI or LLM policy | Pass if no rule bans AI-assisted contributions; pass if no policy is stated | required |
| `good-first-issue-label` | Check the issue labels list in the issue body | Pass if the issue has a good-first-issue or beginner-friendly label | preferred |
| `maintainer-engaged` | Check the comment thread for a maintainer response | Pass if a maintainer commented on the issue within 90 days | preferred |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. Preferred checks never change the verdict; they help rank accepted issues. If any check result is unclear, treat it as fail.
