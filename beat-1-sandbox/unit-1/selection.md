# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72

**Verdict output**

```
Issue #72 — verify_password raises instead of returning False

┌──────────────────────────┬───────┬───────────────────────────────────────────────────┐
│          Check           │ Grade │                     Evidence                      │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ repo-not-archived        │ pass  │ repo API: archived=false                          │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ maintainer-active        │ pass  │ commit 2026-09-16T21:42:18Z                       │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ scope-bounded            │ pass  │ one file (core/security.py), named xfail marker   │
│                          │       │ to remove, "1–2 hours"                            │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ not-claimed              │ pass  │ assignees=[]; one classmate claim comment from     │
│                          │       │ sseid4 (author_association NONE), which per Path  │
│                          │       │ Review house rule does not block; PR search       │
│                          │       │ returned 0 results                                │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ ai-contribution-allowed  │ pass  │ no policy found                                   │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ good-first-issue-label   │ pass  │ labels include 'good first issue'                 │
│ (pref)                   │       │                                                   │
├──────────────────────────┼───────┼───────────────────────────────────────────────────┤
│ maintainer-engaged       │ fail  │ only comment is the classmate's claim,            │
│ (pref)                   │       │ author_association NONE, no maintainer reply      │
└──────────────────────────┴───────┴───────────────────────────────────────────────────┘

Verdict: accept
```

```json
{
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "repo API: archived=false"},
      {"name": "maintainer-active", "grade": "pass", "evidence": "commit 2026-09-16T21:42:18Z"},
      {"name": "scope-bounded", "grade": "pass", "evidence": "body names core/security.py + one test, 'Estimated effort: 1-2 hours', names exact xfail marker to remove"},
      {"name": "not-claimed", "grade": "pass", "evidence": "assignees=[]; one classmate claim comment from sseid4 (author_association NONE), which per Path Review house rule does not block; PR search returned 0 results"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md and PR template contain no AI policy"},
      {"name": "good-first-issue-label", "grade": "pass", "evidence": "labels include 'good first issue'"},
      {"name": "maintainer-engaged", "grade": "fail", "evidence": "only comment is the classmate's claim, author_association NONE"}
    ],
    "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

Run 1: 16/20 (below bar)
Run 2: 18/20 (PASS)
Run 3: 18/20 (final run, saved as eval-run.txt)

**Issue analysis**

issue-19 was the hardest disagreement. My rubric said reject; the gold label said accept. The issue (zxcalc/zxlive#517) described a UI freeze with Priority: High and suggested multiprocessing as a fix. My scope-bounded check initially failed it because the issue mentioned multiple technical approaches and was labeled high priority. After reviewing the gold label, I realized scope-bounded should only reject issues that are explicitly reserved for maintainers or require special access — not issues that simply look complex. The repo was active, unclaimed, and AI-friendly, so all four core families passed.

**Check rationale**

The current scope-bounded check reads: "Read the issue body for explicit blockers only: is it assigned to a specific person, does it require maintainer-only access, or does it explicitly state it is not suitable for outside contributors | Pass if none of those explicit blockers are present; fail only if the issue body explicitly states it is reserved for maintainers or requires special repository access"

I made it this lenient because my earlier stricter version was rejecting valid issues like issue-04, issue-16, and issue-19 — all of which the gold labels accepted. The key insight was that complexity alone does not disqualify an issue; only explicit exclusion of outside contributors does.

**Trade-offs**

The lenient scope-bounded check accepts issue-20 (gold: reject, my verdict: accept), which is the one issue I still get wrong. A stricter check would catch issue-20 but would re-break issue-19. I accepted this trade-off because hitting 18/20 with the category floor met clears the bar, and tightening scope-bounded caused more harm than good across the full set.

---

## Selection rationale

**Selection rationale**

1. Issue #72 fits my interests because it involves a security function (verify_password) and is scoped to a single file (core/security.py) with a clear fix — removing an xfail marker and making the function return False instead of raising an exception. The estimated effort of 1-2 hours fits the time I have available.

2. The skill correctly identified that the issue is unclaimed, the repo is active, and AI contributions are allowed. What the rubric could not weigh is that the fix requires understanding how passlib handles unknown hash formats, which adds a small learning curve beyond what the labels suggest.

3. The main difficulty in claiming it is that one classmate has already commented a claim. The house rules say classmate claims do not block, but I will need to move quickly and make sure my PR is the first one opened.