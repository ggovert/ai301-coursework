# My first open-source pull request: writing a fix for a WeatherGenerator plotting crash

## Overview

This is my first time contributing to something where I can use my skills in Python and data visualization. This lesson helped me so much in learning how to contribute to open source.

It is a contribution to open source. The bug I worked on is in WeatherGenerator, where there is the `len()` problem: it shows an error if we give only one forecast step. So I wrote a fix for that code, and with my fix it shows a warning instead of just throwing an error. The pull request closed without being merged.

I wrote the rubric, and AI helped me refine it. All the final decisions were mine. AI helped me find the repo, consult on whether it was good or not, help finish the bug, and so on.

What I learned is that collaborating with AI is definitely how to push a first open source contribution, and how to use an AI skill to choose an issue that is doable to do, with a bunch of guardrails to make sure we choose the correct issue, in the sense of a repo that is still active.

Pull request: https://github.com/ecmwf/WeatherGenerator/pull/3049

## What happened

### The first scan

The scout checks whether an issue is good enough.

Finding the right issue was hard for me, because a lot of them didn't match my skills and the criteria that I set, so I had to go back and forth.

Real excerpt, scan-notes.md (2026-11-06):

```text
All 5 graded issues were accepted, so the scout was not separating good from bad. Three of the five were off-topic keyword matches: "chart" matched a Helm chart (stigmer#2997), "size-chart" images (myoc#175), and a docs screenshot (DaoCloud-docs#7723).
```

### What I changed, and whether it worked

I kept changing it so that it matched the rubric, based on what I set the answer should be.

Real excerpt, scan-notes.md (2026-11-09):

```text
The fix from 2026-11-07 did not work. The scout again said it found no CONTRIBUTING file at the standard paths for both repos, but WeatherGenerator has CONTRIBUTING.md at its root and cf-plot has .github/CONTRIBUTING.md, and I confirmed both by fetching them myself.
```

### Choosing and reproducing the issue

I chose it because it has a specific problem to solve, I know how to recreate the problem, and it is easy enough to solve for a newbie like me.

Real output, the new test on the unfixed code:

```text
FAILED packages/evaluate/src/weathergen/evaluate/plotting/timeseries_test.py::test_single_forecast_step_saves_plot_and_warns
E       TypeError: object of type 'numpy.datetime64' has no len()
========================= 1 failed, 1 passed in 7.00s ==========================
```

### The fix and the review

Real excerpt, the diff of timeseries.py (commit 0ffd4fc0):

```diff
-        valid_times = da_tars_ts.valid_time.values
+        # With a single forecast step, xr.concat leaves valid_time as a scalar: make it 1-D.
+        valid_times = np.atleast_1d(da_tars_ts.valid_time.values)
+
+        # A single point cannot form a line, so warn and draw it with a marker.
+        single_step = len(valid_times) == 1
+        if single_step:
+            _logger.warning(...)
+        marker = "o" if single_step else None
```

### The plan check

It gave the overall view of how I should tackle the problem and how I should plan it, so that I could send it to the repo to be reviewed.

Real quote, plan-check's output (2026-11-10):

```text
Zero-step claim is unverified. The plan says the zero-step case "fails earlier, in a different place" as fact. I couldn't find anything showing you checked it. Hedge it, or run it.
```

What I got when I ran it:

```text
zero steps: ValueError: must supply at least one object to concatenate
raised from: get_preds_tars_per_region_sample_channel() at line 63 of timeseries.py
```

### How it ended

A maintainer closed the pull request on November 12 without merging it or leaving a comment. I’m still unsure why it was closed. I felt happy that I had reproduced the crash and opened my first open-source pull request.

## Limitations and what's next

I had limited knowledge of the repo that I was working on. Next time I would read the evaluation docs and run a full example before working on the plotting code. Because my pull request was closed, I will also look for other issues related to my skills that I can fix.
