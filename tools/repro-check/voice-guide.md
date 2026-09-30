# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->
I am a student and early-stage contributor working through a structured
reproduction exercise. I have limited history in these repos. Readers
should expect specific, evidence-backed comments and honest reporting
of what I found -- including when I could not reproduce something.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
### Rule: Promise only what I have done or will do next

I do not claim I reproduced something until I have the artifacts to
show it. I do not promise a fix, a timeline, or a follow-up I cannot
commit to.

- Wrong: "I reproduced this and will submit a fix soon."
- Right: "I will attempt to reproduce this against the stated environment and post my findings here."

### Rule: Name the specific behavior, not the category

I reference the exact error, output, or failure mode the issue
describes. Vague references to "the bug" or "the problem" do not tell
readers what I actually saw.

- Wrong: "I was able to see the issue occurring on my machine."
- Right: "I observed the same KeyError on line 42 of parser.py when running the command from the issue."

### Rule: State what I cannot reproduce, not just what I can

If I cannot trigger the behavior, I say so directly and explain what I
tried. Silence or vague hedging is not an honest report.

- Wrong: "I ran the steps but results may vary depending on setup."
- Right: "I could not reproduce this on Python 3.11 with the listed dependencies; the command exited cleanly with no error."

### Rule: Match the repo's required format before posting

I check CONTRIBUTING.md and the issue template before drafting. If the
repo requires AI-use disclosure, I include it. I do not skip required
fields because they feel optional.

- Wrong: Posting a comment with no disclosure in a repo whose policy requires it.
- Right: Including the disclosure line exactly as the repo's policy states before posting.

### Rule: Do not pile on or paraphrase other comments

My repro report uses my own words and my own artifacts. I do not write
"same as above" or quote another commenter's steps as my evidence.

- Wrong: "I can confirm what the previous commenter said -- same issue here."
- Right: Posting my own environment, my own steps, and my own output, even if another person reproduced the same bug.

## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->
- Promises to fix something or deliver by a date
- Reproduction claims without artifacts that show the behavior
- "Same issue" or "can confirm" without my own evidence
- Confident conclusions that go beyond what my output shows
- Comments drafted quickly when tired that skip the conventions check
