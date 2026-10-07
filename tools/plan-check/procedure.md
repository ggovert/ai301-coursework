# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->
Read the package in this order before grading any check. Note the
listed items as you go; they are the inputs to evidence gathering.

1. Read rubric.md and note every check name, its evidence source, its
   pass condition, and its weight. Read references/evidence-guide.md
   and note where each evidence family lives in a plan package. These
   two files define what you are looking for before you look at the
   package.
2. Read the issue context first. Note the reported behavior, any
   maintainer comments, and any suggested directions. Reading the issue
   first means the repro evidence and the plan can be judged against
   what was actually reported, not assumed.
3. Read the repro-evidence block. Note the exact commands run, the
   observed output or error, and the environment. This pins down the
   behavior the plan must explain. If no repro-evidence block exists,
   note its absence; several checks depend on it.
4. Read the repo-facts block. Note the files and functions listed, the
   contribution policy, any AI-use disclosure requirement, and any
   issue or PR templates.
5. Read the candidate plan. Note the stated cause, scope statement,
   files to touch, approach, test plan, and risks and unknowns section.
6. Read the candidate plan comment. Note what it says about the
   approach and how it addresses the thread.

Do not grade any check until all six parts have been read and noted.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->
Gather evidence for each family before running the checks that use it.
Record a direct quote or a specific absence for each item.

1. Diagnosis evidence: from the plan's diagnosis section, copy the
   stated cause. From the repro-evidence block, copy the observed
   behavior (error message, output line, or failure description) that
   the cause must explain.
2. Cause-vs-symptom evidence: from the plan's approach section, copy
   what will be changed and where. From the repro-evidence block, note
   whether the failure originates at that location or upstream of it.
3. Scope evidence: from the plan's scope statement, copy the in-scope
   description and any not-in-scope line. From the files-to-touch list,
   copy every file named.
4. Executability evidence: from the files-to-touch list and approach,
   copy every file and function named. From the repo-facts block,
   confirm whether each named file exists. Note any file that does not
   appear in the repo-facts block.
5. Test plan evidence: from the plan's test plan section, copy the
   steps and the stated success condition. From the repro-evidence
   block, copy the original steps and observed output.
6. Honesty evidence: from the risks and unknowns section, copy
   everything listed. From the diagnosis and approach sections, copy
   every claim stated as settled fact.
7. Comms evidence: from the plan comment, copy the full text. From
   the issue context, copy any maintainer signals or suggested
   directions. From the repo-facts block, copy the contribution policy
   and any required templates or disclosures.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

Run checks in the order they appear in the rubric. Each check uses
only the evidence gathered in the previous stage; do not re-read the
package during check execution.

1. diagnosis-matches-repro: compare the stated cause against the
   observed behavior from the repro-evidence block. Pass if the cause
   is consistent with and would explain the observed behavior. Fail if
   it contradicts the evidence, ignores it, or only restates the
   symptom. If the repro-evidence block is absent, grade unclear.
2. cause-not-symptom: compare the approach's change location against
   where the repro evidence shows the failure originates. Pass if the
   change targets the origin. Fail if it targets only where the failure
   surfaces while the evidence points upstream. If the origin cannot be
   determined from the evidence, grade unclear.
3. scope-bounded: check the scope statement and files list. Pass if
   one bounded change is described and at least one exclusion is named.
   Fail if no limit is stated, unrelated work is included, or no files
   are listed.
4. stranger-can-start: check each named file against the repo-facts
   block. Pass if every file exists in the repo-facts block and the
   approach gives a clear order of work. Fail if any file is absent
   from the repo-facts block, or if the approach is too vague to begin
   without asking the author. If the repo-facts block lists no files at
   all, grade unclear.
5. test-plan-observable: compare the test plan's steps and success
   condition against the repro-evidence block's steps and output. Pass
   if the test plan re-runs the repro steps and names a specific
   observable difference. Fail if success is stated only as "tests
   pass," "it works," or another non-observable condition.
6. unknowns-honest: compare the risks and unknowns list against the
   settled claims in diagnosis and approach. Pass if every unverified
   claim is labeled as a guess or open question and not stated as fact
   elsewhere. Fail if confident claims appear in the plan alongside an
   empty or missing risks section.
7. comment-fits-thread: compare the plan comment against the
   maintainer signals in the issue context and the conventions in the
   repo-facts block. Pass if the comment responds to what the thread
   contains, follows the repo's conventions, and includes any required
   disclosures. Fail if it ignores maintainer signals, skips required
   fields, or reads as boilerplate that could be pasted onto any issue.

When evidence for a check is genuinely absent from the package, grade
that check unclear. Do not invent evidence or assume it exists
elsewhere.


## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->
1. Collect the grade for every check: pass, fail, or unclear.
2. Treat every unclear as a fail, as the rubric's verdict rule states.
3. If every required check is pass, the verdict is accept.
4. If any required check is fail or unclear, the verdict is reject.
5. Preferred checks never change the verdict; record their grades but
   do not apply them to the verdict rule.
6. In the output, quote the evidence line from the first failing
   required check as the deciding evidence. If multiple checks fail,
   list all of them in the checks array and quote the first in the
   summary.
7. Emit the verdict as the last fenced JSON block in the output, as
   SKILL.md requires.