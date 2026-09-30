# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

**Where it lives:** In the repro report, in a dedicated environment
section or block near the top. In an eval bundle, look for OS, runtime
version, and dependency versions listed before or alongside the
reproduction steps. In live mode, check the draft comment directly;
for the issue's target environment, look at the issue body and any
linked CI config or README in the repo-facts block.

**What good looks like:** The report names the operating system,
runtime version (e.g., Python 3.10.12), and the versions of any
dependencies the issue references. If the reporter's environment
differs from the issue's stated target, the difference is called out
("I used Node 20 rather than the Node 18 the issue names"). A record
that lists only "Python" with no version, or omits the OS entirely, is
not sufficient.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

**Where it lives:** In the repro report's steps section, as a numbered
or ordered list. In an eval bundle, look for the sequence between the
environment record and the output artifacts. In live mode, read the
draft comment's steps block.

**What good looks like:** Each step starts from a stated beginning
state (fresh clone, a specific command run first, a particular file in
place). Steps are ordered and specific enough that a stranger with the
stated environment can follow them without inferring missing actions.
A step like "run the app" is not followable; "run `python main.py
--config config.yaml` from the repo root" is.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->
**Where it lives:** In the repro report's output section -- error
messages, log excerpts, screenshots, or terminal output pasted or
linked directly in the comment. In an eval bundle, look for a fenced
code block or quoted output after the steps. In live mode, check the
draft for attached artifacts or inline output.

**What good looks like:** The artifact shows the same error message,
failure mode, or output the issue describes -- not a related failure
on a different code path. If the issue names a specific exception or
line number, the artifact shows that exception or confirms the same
line. An artifact that shows a different error, or no error when one
is expected, does not pass this check even if something went wrong.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

**Where it lives:** In the repro report's conclusion or summary -- the
sentence or short paragraph that states what the reporter found. In an
eval bundle, look for the closing statement after the artifacts. In
live mode, read the final lines of the draft.

**What good looks like:** The conclusion matches the artifacts exactly.
If the output shows the bug, the conclusion says so and points to the
artifact. If the reporter could not reproduce it, the conclusion says
"I could not reproduce this" and describes what they observed instead.
A conclusion that claims reproduction without an artifact showing the
behavior, or that hedges ("results may vary") without saying what
actually happened, fails this check.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->
**Where it lives:** The claim comment and repro report text, read
against the repo-facts block. In an eval bundle, the repo-facts block
contains the relevant CONTRIBUTING.md excerpt, issue template, and any
AI-use disclosure policy. In live mode, check the repo's
CONTRIBUTING.md, issue template, and any policy file the repo links
from its issue creation page.

**What good looks like:** The comment follows any required template
structure (fills in required fields, does not delete required
headings). If the repo's policy requires AI-use disclosure, the
comment includes it in the form the policy specifies. The claim
comment names the specific issue by its behavior or title, not just
its number, and states what the author will investigate -- not what
they will fix or when.