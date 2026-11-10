# Contribution: timeseries plots crash for single forecast step

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Giovanni Govert
**GitHub Username:** ggovert
**Issue:** https://github.com/ecmwf/WeatherGenerator/issues/2985
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: issue-scout with my own search strategy, patched after its first scan and first grade**

I built issue-scout from my unit 1 skill: I wrote a six-sentence fit profile, a set of gh search queries and ranking rules in search-strategy.md, and my first scan accepted all five issues it graded, but three were off-topic keyword hits (a Helm chart, size-chart images, and a docs screenshot). I fixed that by switching to title-only queries with more specific words (plot, matplotlib, visualization), adding direct queries for Streamlit, plotly.py and recharts, and adding a ranking rule that drops docs, screenshot and Helm titles; I tested those fixes on live results with a script rather than paying for a second scan. When I graded my pick, ecmwf/WeatherGenerator#2985, the scout accepted it but wrongly said the repo had no CONTRIBUTING.md, because the repo does have one plus a pull-request template that asks for an LLM review. I caught that by reading the repo's files myself and rewrote the ai-contribution-allowed check to name every path it must fetch, but when I regraded two days later the scout still said it found no CONTRIBUTING file in either of my picks, so the fix did not work and the check is not yet reliable on a repo that has a real policy to find.

**Unit 6: a voice-guard hook with upstream rules, and a local memory file for the repo**

I installed the voice guard as a hook in my global Claude Code settings, added four upstream rules to my voice guide (claims, questions, pings), and wrote a 26-line `CLAUDE.local.md` for my fork of ecmwf/WeatherGenerator. The shipped hook calls `python3`, which on my laptop is the Microsoft Store stub, so it would have failed silently and protected nothing; I pointed it at my real Python path instead, and I used pointer files for the shared voice guide because symlinks do not work reliably on Windows. The wiring test passed (the guard stopped `gh issue comment --help`), and it passed my claim draft by hand-run check, but I have not yet seen it stop a real draft, and I posted the claim from the browser, where the guard cannot see it. My first version of the memory file also came out wrong, because my shell quoting stripped every command in backticks; I caught it by reading the file back and rewrote it.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I started with my scout. My fit profile says I use Python and SQL, I have built React and Next.js sites, and I like fixing UI, chart and visualization bugs. My first scan returned five issues that the rubric accepted, but none of them was a good match: three were off-topic keyword hits (a Helm chart, size-chart images and a docs screenshot). I fixed my queries and filters, and then searched again with a script that used those queries and also checked each repo's health, such as whether PRs from several different people had been merged recently. That search found ecmwf/WeatherGenerator#2985, "timeseries plots crash for single forecast step". So the issue did not come from the scout's scan itself: it came from my own search, and I then graded it with the scout. I also looked at the AI301 Issue Selection site, but I could not find an issue that fit my skills, and the ones I liked were already claimed, so I asked my instructor, who agreed I could use this one.

I graded #2985 and a second candidate, NCAS-CMS/cf-plot#151, with the scout in direct mode, and it accepted both: neither has a good-first-issue label and neither has a maintainer comment yet, but every required check passed. I chose #2985 because it is a Python plotting bug in an active project (commits within the last few days, several different people merging PRs), nobody had claimed it, and the cause is already traced: with one forecast step, `xr.concat(..., coords="different")` leaves `valid_time` as a scalar and `len()` fails. My grades came back before I added the scope patch, so there is no difficulty note from the scout. By my rubric's own definitions it would be "ambitious", because the maintainer's wording leaves one design choice open (warn and skip the plot, or warn and draw a single point). The fix itself looks small, and I raised that choice as a question in my claim, as the note says to. I hope to learn how xarray joins data, how to write a test for a plotting function, and how a real project reviews a pull request.

How the scout did: it was weakest where I needed it most. Its first scan accepted everything, including the off-topic hits, and on both of my picks it said it found no CONTRIBUTING file, which was wrong for both repos (one has CONTRIBUTING.md at the root and the other has it in .github/). I rewrote that check once and the scout still got it wrong, so I do not trust that check yet. What held up was the required checks on repo activity and claims, because I confirmed them by hand with `gh` and they matched.

My claim comment: https://github.com/ecmwf/WeatherGenerator/issues/2985#issuecomment-6764353493 (posted 2026-11-10).

**Toolkit**

- Tool: issue-scout, with my own search strategy and rubric. I used it for one scan and then two direct grades, and I swapped in the staff scope patch in unit 6.
- What it produced: a scan of five accepted but mostly off-topic issues, then an accept verdict on #2985 and on cf-plot#151, with every required check passing and both preferred checks (good-first-issue label, maintainer comment) failing.
- Difficulties: the scan did not separate good issues from bad ones; the AI-policy check said it found no CONTRIBUTING file in either repo, though both have one; and the issue I chose came from my own search, not from the scan.
- What changed: I rewrote my queries and ranking filters, replaced my `scope-bounded` check with the staff `scope-feasible` row and added the difficulty note (2026-11-09), and rewrote the AI-policy check's evidence, which did not fix it. I would next name the exact `gh api` fetch in that check and make the scout quote a line from the file it finds.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

- Operating system: Windows 11 Home, running the project inside WSL 2 with Ubuntu 24.04.1 LTS. The project lists only Linux and macOS as supported platforms, so Windows itself was not an option.
- Versions: Python 3.12.3 (the project requires `>=3.12,<3.13`), uv 0.13.7, xarray 2026.4.0, numpy 2.4.4, matplotlib 3.10.9. Project: ecmwf/WeatherGenerator, `develop` branch, commit `6608f5af9bbf5711b8282b4488fe4774eeea3022` (2026-11-05).
- Setup: cloned the repo and ran `uv sync --package weathergen-evaluate --group dev`, which installs only the evaluate package and its test tools. I did not use the documented `./scripts/actions.sh sync`, because it installs GPU extras (flash-attn, CUDA torch) that a laptop without a GPU does not need.
- Challenges: the evaluate package still pulled in torch and flash-attn as dependencies (the uv cache passed 5 GB during the download), so the sync was slow, but it finished with exit code 0 and no errors. No compiler problems came up.

**Steps to Reproduce**

1. In the repo root, use the environment from the sync above (`.venv/bin/python`).
2. Save a short script as `repro_real.py` that builds small synthetic prediction and target data (one channel, two samples, five points per step) and calls the real `Timeseries.plot_single_timeseries` with 2 forecast steps and then with 1. The full script is in the Reproduction Evidence below.
3. Run `.venv/bin/python repro_real.py`.
4. Observed result: the 2-step call saves a plot; the 1-step call raises the `TypeError` from the issue.

**Reproduction Evidence**

- **Commit showing reproduction:** none (nothing committed to my fork yet).
- **Screenshots/logs:** output of `repro_real.py`, run on 2026-11-10 against `develop` at `6608f5a`:

```
2 forecast step(s): plot OK
1 forecast step(s): CRASH -> TypeError: object of type 'numpy.datetime64' has no len()
```

```python
import sys, tempfile, numpy as np, xarray as xr
from weathergen.evaluate.plotting.timeseries import Timeseries

def make(step):
    t = np.datetime64("2026-01-01T00") + np.timedelta64(6 * step, "h")
    n = 5
    return xr.DataArray(
        np.random.rand(n, 2, 1),
        dims=("ipoint", "sample", "channel"),
        coords={"ipoint": np.arange(n), "sample": [0, 1], "channel": ["z_500"],
                "valid_time": ("ipoint", [t] * n)},
    )

for nsteps in (2, 1):
    preds = {f"step{s}": make(s) for s in range(nsteps)}
    tars = {f"step{s}": make(s) for s in range(nsteps)}
    out = tempfile.mkdtemp()
    try:
        Timeseries(preds, tars).plot_single_timeseries(out, "z_500", 0, "ERA5", "global")
        print(f"{nsteps} forecast step(s): plot OK")
    except Exception as e:
        print(f"{nsteps} forecast step(s): CRASH -> {type(e).__name__}: {e}")
```

A second, xarray-only script (`repro_concat.py`) copies the `.sel`/`.mean`/`.concat` steps of `get_preds_tars_per_region_sample_channel` and checks the cause on its own, with the same environment:

```
1 step(s): valid_time ndim=0 shape=() -> len() FAILS: object of type 'numpy.datetime64' has no len()
2 step(s): valid_time ndim=1 shape=(2,) -> len() = 2
```

- **My findings:** the crash reproduces with the same error message as the issue, in the project's own `plot_single_timeseries`, at `len(valid_times)` (line 97 of `packages/evaluate/src/weathergen/evaluate/plotting/timeseries.py`). The cause the issue describes holds up: with one forecast step, `xr.concat(..., coords="different")` has nothing to stack, so `valid_time` stays a scalar. What this does not show: I used synthetic data, not the project's zarr output, and I called the plotting class directly instead of running the full `evaluate` command with the issue's config, so I cannot confirm every step of the issue's traceback, only the failing function. I did not test ensembles (`ens`), several channels, or regions other than "global".

**Toolkit**

- Tool: repro-check, switched to its real-repo scope in unit 6. I ran it on my claim comment and this report together.
- What it produced: an accept verdict with all seven checks passing, plus voice-guide notes. One note was right: my report mentioned the xarray-only check without including its script or output, so I added both.
- Difficulties: another note was wrong. It said my posted claim still started with "Assign me" and had no output block, and suggested editing the comment with `--edit-last`. I fetched the live comment and compared it with my draft: they were identical and the comment had never been edited, so I did not edit it.
- What changed: I added the xarray-only script and its output to the report. Next time I will fetch the live text myself before acting on a note about what was posted.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
