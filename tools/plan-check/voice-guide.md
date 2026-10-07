# Voice guide: how I talk upstream


## Who I am in threads

I am a student and early-stage contributor working through a structured
reproduction and planning exercise. I have limited history in these repos. Readers
should expect specific, evidence-backed comments and honest reporting
of what I found -- including when I could not reproduce something.

## Rules I write by

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

### Rule: State the approach at the confidence I actually have

I label what I verified and what I am guessing. A diagnosis I confirmed
with repro output is stated as fact. A cause I have not confirmed is
stated as my current best reading.

- Wrong: "The bug is caused by the missing null check in utils.py."
- Right: "My repro shows the crash at line 42. I believe the cause is a missing null check in utils.py, but I haven't confirmed that yet."

### Rule: Say what I will change and what I will not

A plan comment names one bounded change and at least one thing I am
leaving out, so maintainers can redirect me before I build.

- Wrong: "I'll clean up the parser while I'm in there."
- Right: "I will change only the null handling in `parse_row`. I won't touch the tokenizer or the CLI flags."

### Rule: Answer maintainers who already suggested a direction

If a maintainer or earlier commenter proposed an approach, I respond to
it directly: I adopt it, or I explain with my own evidence why I am
choosing differently. I never ignore it, and I never write "same
approach as above."

- Wrong: A plan comment that ignores the maintainer's suggestion in the thread.
- Right: "You suggested fixing this in the loader. My repro shows the bad value is already wrong before it reaches the loader, so I plan to fix it at the source. Tell me if you'd rather I go through the loader."

## Things I never post

- Promises to fix something or deliver by a date
- Reproduction claims without artifacts that show the behavior
- "Same issue" or "can confirm" without my own evidence
- Confident conclusions that go beyond what my output shows
- Comments drafted quickly when tired that skip the conventions check
- Timelines or delivery dates for the fix
- A claim that the fix works before I have built and tested it
- A plan that restates the issue title instead of my own diagnosis and evidence
