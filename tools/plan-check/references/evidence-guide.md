# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->
Where it lives:
- Eval bundle: the plan's diagnosis section holds the stated cause.
  The repro-evidence block holds the observed behavior: the exact
  commands run, the error message or output, and the environment.
- Live mode: the plan's diagnosis section in plan.md, and the
  student's posted repro comment on the issue thread, which contains
  the artifacts (commands, output, screenshots) that pin down the
  behavior.

What good looks like: the stated cause names a specific behavior or
code location that the repro evidence actually shows, and it would
explain every symptom in that evidence. A diagnosis that contradicts
the evidence, ignores part of it, or only restates the symptom ("the
button is broken") is not grounded. Good: "the crash on line 42 occurs
because parse_row receives a None value when the input file is empty,
as shown in the repro output." Bad: "the parser fails when given bad
input."

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

Where it lives:
- Eval bundle: the plan's scope statement and its in-scope and
  not-in-scope lines. The files-to-touch list, which may appear as a
  bullet list or a table in the plan.
- Live mode: the same sections in plan.md in the student's fork clone.

What good looks like: one change described in a sentence, with at
least one thing explicitly named as out of scope. A drive-by rewrite
shows up as extra files added without connection to the diagnosis,
cleanup tasks bundled in, or no stated limit at all. Good: "I will
change only the null check in parse_row in parser.py. I will not touch
the tokenizer or the CLI." Bad: "I'll fix the parser and clean up some
related code while I'm in there."

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

Where it lives:
- Eval bundle: the plan's files-to-touch list and approach section,
  checked against the repo-facts block, which lists the files and
  functions that exist in the repo.
- Live mode: the files-to-touch list and approach section in plan.md,
  checked against the actual repo on GitHub.

What good looks like: every file and function named in the plan exists
in the repo-facts block, and the approach gives a clear order of work
a stranger could follow. Good: "open parser.py, find parse_row at line
38, add a None check before the split call." Bad: "update the relevant
parsing logic to handle edge cases." If a named file does not appear
in the repo-facts block, that is a fail signal regardless of how
detailed the approach is.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

Where it lives:
- Eval bundle: the plan's test plan section, read against the
  repro-evidence block's steps and observed output.
- Live mode: the test plan section in plan.md, read against the
  student's posted repro comment on the issue thread.

What good looks like: the test plan re-runs the exact steps from the
repro evidence and names a specific observable difference between
before and after the fix, such as a changed error message, a different
exit code, or output that previously crashed now completing cleanly.
Good: "run `python parse.py empty.csv`; before the fix, expect
KeyError on line 42; after the fix, expect clean exit with zero rows
parsed." Bad: "run the tests and verify it works" or "confirm the bug
is gone."

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

Where it lives:
- Eval bundle: the plan's risks and unknowns section, read against
  the claims in the diagnosis and approach sections. In live mode,
  also the ## Deviations heading at the end of plan.md, which is where
  an honest mid-build change gets recorded.
- Live mode: the risks and unknowns section and the Deviations heading
  in plan.md.

What good looks like: things the author has not verified are labeled
as guesses or open questions and are not stated as fact elsewhere in
the plan. Good: "I believe the cause is the missing null check, but I
have not confirmed whether the same path is reached when the file has
one row." Bad: a confident diagnosis with no risks section, or a risks
section that says only "none identified." A Deviations heading left
blank after the build is also a fail signal for honesty.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

Where it lives:
- Eval bundle: the candidate plan comment, read against the thread
  highlights in the issue context and against the repo-facts block,
  which contains the contribution policy, any required templates, and
  any AI-use disclosure requirement.
- Live mode: the draft comment in comment.md, read against the live
  issue thread on GitHub and against CONTRIBUTING.md or the repo's
  stated conventions.

What good looks like: the comment responds to what the thread actually
contains, including any maintainer suggestions or questions, follows
the repo's stated conventions and templates, and includes any required
disclosures such as AI-use. Good: a comment that names the diagnosis
from the student's own repro, addresses a maintainer's suggestion
directly, and includes the required disclosure line. Bad: a comment
that could be pasted unchanged onto a different issue, ignores a
maintainer's suggested approach, or skips a required field.