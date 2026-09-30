# Rubric: 

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment section (OS, language/runtime version, dependency versions, any relevant config) read against the versions or platform named in the issue | The report names the OS, runtime, and key dependency versions; if they differ from the issue's target, the difference is called out explicitly | required |
| Steps are followable | The reproduction steps in the repro report, read as a stranger starting from a fresh clone | A stranger can follow the steps from the stated starting state to the trigger without filling in any gaps; a file whose contents can be inferred from the issue description or the report's own description passes -- only a file referenced with no description at all fails this check | required |
| Behavior matches issue | The output excerpts, logs, or screenshots in the repro report read against the error or behavior the issue describes | The artifact shows the issue's behavior OR the report honestly states it could not reproduce the behavior, documents what was tried, and explains what differed from the issue's conditions | required |
| Outcome stated honestly | The conclusion section of the repro report read against the artifacts shown | The report's conclusion matches what the artifacts actually show; a cannot-reproduce is reported as such with the evidence, not glossed over or omitted | required |
| Conventions followed | The claim comment and repro report read against the repo-facts block (CONTRIBUTING.md, issue template, AI-use disclosure policy) | The comments follow any required template structure and include any required AI-use disclosure; no required field is skipped | required |
| AI disclosure | The repo-facts block read for any AI-use disclosure policy in CONTRIBUTING.md or a dedicated AI policy file | If the repo requires disclosure for issue comments, the comment includes a statement naming the tool and extent of use; if the policy explicitly states no disclosure is required for issue comments, this check passes | required |
| Claim names the issue | The claim comment read against the issue title and description | The claim comment references the specific issue by its behavior or title; states what the author will do next; if the author has already reproduced, they may say so -- the rule is only that they must not promise reproduction they have not yet done | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept if every required check passes. A single required check that fails or is unclear holds the package. Unclear counts as fail: proof that cannot be verified is not ready to post. Preferred checks never change the verdict.
