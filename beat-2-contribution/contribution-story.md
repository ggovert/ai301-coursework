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
**Pull Request:** https://github.com/ecmwf/WeatherGenerator/pull/3049

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

I installed the voice guard as a hook in my global Claude Code settings, added four upstream rules to my voice guide (claims, questions, pings), and wrote a 26-line `CLAUDE.local.md` for my fork of ecmwf/WeatherGenerator. The shipped hook calls `python3`, which on my laptop is the Microsoft Store stub, so it would have failed silently and protected nothing; I pointed it at my real Python path instead, and I used pointer files for the shared voice guide because symlinks do not work reliably on Windows. The wiring test passed (the guard stopped `gh issue comment --help`), it passed my claim draft in a hand-run check, and it passed the claim again when I posted it through Claude Code (the guard log shows a hook pass at 03:56), but so far it has only stopped the body-less wiring test, so I have not yet seen it stop a real draft. My first version of the memory file also came out wrong, because my shell quoting stripped every command in backticks; I caught it by reading the file back and rewrote it.

**Unit 7: a ship-gate whose manifest runs the project's checks through WSL**

I installed the ship-gate and wrote a four-row manifest (ruff format check, ruff check, `pytest src/`, and my new test file), each row calling into WSL because the project only supports Linux. Two things fought me: `python3` is the Microsoft Store stub on my laptop, so I patched the hook command, and the gate runs its rows from Windows `cmd.exe`, which silently falls back to `C:\Windows` when the clone is inside WSL; I found that with a small test script before relying on the install and recloned my fork on the Windows side, keeping only the Python environments in WSL. On my real branch the gate passed twice (all 4 repo checks and all 6 pr-precheck checks); its notes made me reword one sentence and say in the PR that pylint and the type check were not run, and the PR then opened through it. The integration tests are in the manifest's excluded table with a dated reason, because they need a GPU build I cannot install.

**Unit 8: a PR monitor with a playbook built from this repo's real wait times**

I installed the PR monitor and wrote my four-section playbook, and for the staleness threshold I measured the repo instead of guessing: among 11 PRs from authors with no prior relationship only 1 got a maintainer reply (after 0.3 days), `CONTRIBUTING.md` states no wait, so I chose 14 days of quiet before one nudge and 30 more days before I would close my own PR. The monitor read PR #3049 (checks passing, review required, no comments) and drafted "No nudge yet" with the date the 14 days run out (2026-11-25), which was the right move for a PR that is under a day old; it did not draft a reply, because no maintainer has answered, so I cannot yet say how it handles real feedback. Along the way my first wait-time script was wrong twice (the `gh pr list` command has no author-association field, and GitHub labels some team members "CONTRIBUTOR", which made them look like outsiders), so I switched to the REST API and filtered to authors with no relationship, and the sample is still small and may undercount replies. The monitor also wrote a cosmetic encoding glitch ("nudgeâ€¦") into its draft, which I noted and did not need to fix.

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

When someone asks WeatherGenerator's evaluation tool to plot a timeseries for only one forecast step, the program crashes instead of producing a plot or a clear message. A timeseries needs several points over time, and the plotting code assumes it always gets a list of dates.

**Expected Behavior**

The program should not crash. The maintainer who opened the issue asks for it to "fail gently with a warning saying that there are not enough fsteps specified", so the user learns what happened.

**Current Behavior**

The plot raises `TypeError: object of type 'numpy.datetime64' has no len()` at `timeseries.py` line 97, and the evaluation run stops. I reproduced the same error on `develop` with small synthetic data: two forecast steps save a plot, and one step crashes.

**Affected Components**

`packages/evaluate/src/weathergen/evaluate/plotting/timeseries.py`: `Timeseries.get_preds_tars_per_region_sample_channel` (where one step leaves `valid_time` as a single value) and `Timeseries.plot_single_timeseries` (where `len(valid_times)` fails). It is called from `_dispatch_timeseries_plots` in `plot_orchestration.py` and run through `dispatch_parallel` in `io/data/io_orchestration.py`.

**Toolkit**

- Tool: my `CLAUDE.local.md` repo memory file, plus `gh` to read the issue thread and the repo's files.
- What it produced: a fast route to the three files that matter, and the exact commands for lint and tests, so I did not have to rediscover them in every session.
- Difficulties: the memory file said tests live in the root `tests/` folder, which was only half true: the repo keeps unit tests next to the code as `*_test.py` files, and CI's `pytest src/` does not look inside `packages/`.
- What changed: I corrected my understanding while building the test; I have not yet updated the memory file.

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

With one forecast step, `get_preds_tars_per_region_sample_channel` joins the per-step series with `xr.concat(..., coords="different")`. With only one input there is nothing "different" to stack, so the `valid_time` coordinate stays a single value instead of a 1-element array. `plot_single_timeseries` then reads `valid_times = da_tars_ts.valid_time.values`, a 0-dimensional array, and line 97 calls `len(valid_times)` to choose the date tick spacing, which raises the `TypeError`. With two or more steps `valid_time` is 1-D and the same code works. I confirmed this on `develop` at `3508fa98` with a script that calls the real `plot_single_timeseries` (2 steps saves a plot, 1 step crashes) and with a separate xarray-only script that shows `valid_time` has shape `()` for one step and `(2,)` for two.

**Proposed Solution**

Change only `plot_single_timeseries`: wrap `valid_times` with `np.atleast_1d`, and when there is only one forecast step, log a warning through the module's logger and still draw the point with a marker (a line through one point is invisible). That is the same pattern `bar_plots.py` already uses when it has fewer than two runs: warn, then continue. Add a `timeseries_test.py` next to the module with two tests. I am deliberately not changing the `xr.concat` call, the zero-step case (I ran it: `get_preds_tars_per_region_sample_channel` raises `ValueError: must supply at least one object to concatenate` at line 63, before the plot code runs, so it is a separate problem), the parallel-dispatch fallback, or any other plot. The issue says to "fail gently with a warning"; I chose warn-and-draw and asked the maintainer in my claim comment whether they prefer skipping the plot, so I will follow their answer if one comes. Risks I wrote down: the maintainer may want a different approach, I only used synthetic data (no ensembles, several channels or other regions), and CI may not collect my test.

**Implementation Plan**

1. In `timeseries.py`, add `import logging`, `import numpy as np`, and the module `_logger`.
2. In `plot_single_timeseries`, wrap `valid_times` with `np.atleast_1d`, add the single-step warning, and pass a `marker` to both `ax.plot` calls.
3. Add `timeseries_test.py` with a one-step test (it must fail before the fix) and a two-step test.
4. Run the check-only lint, the project's unit tests and my new test, then re-run the reproduction for before and after evidence, and open the PR against `develop` with `Closes #2985`.

Deviations: I first expected the repo's tests to live in the root `tests/` folder, but it keeps them next to the code as `*_test.py` files, so I put mine beside `timeseries.py`. CI's `pytest src/` does not collect anything under `packages/`, so I run my test file directly and say so in the PR. After an LLM review of my diff, I also changed the single-step condition from `< 2` to `== 1`, because the warning would have said "one forecast step" for zero points too.

**Toolkit**

- Tool: plan-check, using its real-repo scope from unit 6, on `plan.md` and a short `plan-comment.md` that I did not post.
- What it produced: an accept verdict with all seven checks passing, plus a list of things to fix. The useful catches were a claim I had stated as fact without checking (that the zero-step case fails somewhere else), a plan with no risks or deviations sections, a stale tense in the comment, and a pronoun I had assumed for the maintainer.
- Difficulties: the tool's own procedure and rubric disagree on the `unknowns-honest` check: the procedure would fail a plan with confident claims and no risks section, while the rubric passed mine, so I had to follow the rubric's verdict and still act on the procedure's concern.
- What changed: I ran the zero-step case (it raises `ValueError: must supply at least one object to concatenate` at line 63, which confirmed the claim), added "Risks and unknowns" and "Deviations" sections, switched to "the maintainer", and gave the plan comment the output line and the AI-use line.

---

## Testing Strategy

1. **Reproduction, before and after.** The same script (calls the real `Timeseries.plot_single_timeseries` on small synthetic data) crashed with `TypeError: object of type 'numpy.datetime64' has no len()` before the fix. After the fix it prints `OK` for both 2 steps and 1 step, plus the new warning, and saves two charts. I opened the one-step chart and the point is visible (this was my main worry, because a line through one point draws nothing).
2. **A test that fails without the fix.** `timeseries_test.py` has a one-step test (a plot file exists, is not empty, and the warning was logged) and a two-step test (a plot file exists and no warning is logged). On the unfixed code the one-step test failed with the exact `TypeError` (1 failed, 1 passed); after the fix both pass (2 passed).
3. **The repo's own checks.** `ruff format --check` and `ruff check` (ruff 0.12.2, as the project pins) pass on `src/ scripts/ packages/`, and the project's unit tests (`pytest src/`, in an environment with the torch CPU extra) pass, 3 tests. I did not run the integration tests (they need a GPU build and do not touch this plot), the experimental type check, or pylint.

What this does not prove: I used synthetic data, not the project's forecast files, and I did not test ensembles, several channels or other regions.

**Toolkit**

- Tool: the ship manifest, run by the ship-gate, plus ruff and pytest in WSL.
- What it produced: four green checks (format check, lint, `pytest src/` with 3 passed, and my test file with 2 passed) that the gate ran on its own before the PR, and a dated excluded table for the checks I could not run.
- Difficulties: `pytest src/` first failed with `ModuleNotFoundError: No module named 'torch'`, because my evaluate-only environment lacks the root package's torch CPU extra, so I built a second environment (with `--frozen`, so the lockfile stayed untouched) just for that row.
- What changed: I pointed the unit-test row at the second environment, and listed integration tests, the type check and pylint as excluded, each with a reason I had checked.

---

## Implementation Notes

**2026-11-07**

Installed the project's evaluate package in WSL (a large download, because it pulled in torch) and wrote a script that calls the real `plot_single_timeseries` on small synthetic data. It reproduced the issue's `TypeError`. I decided to use synthetic data, because the issue's real data lives on an ECMWF machine.

**2026-11-10**

Posted my claim on the issue at 03:56. In the evening I found that the ship-gate cannot work with a clone inside WSL (Windows `cmd.exe` falls back to `C:\Windows` for those paths), so I recloned my fork on the Windows side and rebuilt the Python environment in WSL. I wrote the test first and watched it fail on the unfixed code (1 failed, 1 passed), then made the fix, and ruff flagged two style problems in my own test file, which I fixed. A separate Claude session reviewed the diff and I changed `< 2` to `== 1`; plan-check made me actually run the zero-step case instead of asserting it. The ship-gate passed, I pushed the branch to my fork, and PR #3049 opened at 22:21. Wrong turns: my first run of the project's unit tests failed for lack of torch, and I had assumed the repo's tests live in a root `tests/` folder when they sit next to the code.

**Toolkit**

- Tool: Claude Code with my `CLAUDE.local.md` repo memory, working through the manifest's commands, ruff and pytest.
- What it produced: the fix, the test, the plan files and the PR text, with each step checked by a command instead of by my say-so.
- Difficulties: moving between Windows and WSL shells broke my quoting several times, and one of those errors stripped the commands out of my memory file. The Windows and Linux split also forced the reclone.
- What changed: I put commands in small script files instead of long one-liners, read files back after writing them, and kept the code on the Windows side with the environments in WSL.

---

## Pull Request

**PR Link:** https://github.com/ecmwf/WeatherGenerator/pull/3049

**PR Description:** "[2985][eval] Plot a single point with a warning for one forecast step", 2 files changed (+75 / -3), closes #2985. It explains the cause (one forecast step leaves `valid_time` as a scalar, so `len(valid_times)` fails), the fix (`np.atleast_1d`, a warning, and a marker so the single point is visible), the new test, the before and after output, the checklist from the repo's template with every item answered, what I could not run (integration tests, pylint, the type check), a note that CI's `pytest src/` does not collect tests under `packages/`, and an AI-assistance section. The full text is in the PR.

**Maintainer Feedback:**

- 2026-11-10: none yet. The one automatic check that has run passed, and my claim comment on the issue is still unanswered.

**Status:** Awaiting review

**Toolkit**

- Tool: the ship-gate hook with my pr-precheck, and my voice guard, which both checked the PR before it opened.
- What it produced: a PASS every time it ran (4 of 4 repo checks and 6 of 6 pr-precheck checks), a voice guard pass logged at 22:21, and a PR whose body is character for character the file I had checked.
- Difficulties: my first attempt at the command failed because the `--allowedTools` flag swallowed the prompt (a flag-order mistake), and the gate's pass goes stale when anything changes, so I re-ran it after editing the PR text.
- What changed: I put the prompt before the flag, and re-ran the gate right before opening, which also led me to add a line about pylint and the type check not being run.

---

## Learnings and Reflections

**Technical Skills Gained**

The biggest lesson was that a first open source contribution works best as a collaboration with AI. I used an AI skill (my scout and its rubric) to choose an issue I could actually finish, and it came with guardrails that kept me from picking a bad one: the repo must not be archived, a maintainer must have committed recently, nobody may already be on the issue, and the repo must not ban AI-assisted work. Those checks only helped because I confirmed each one myself with `gh` instead of trusting the tool's word, which is how I caught the scout's wrong "no CONTRIBUTING file" answers. Then I worked with Claude to reproduce the bug, write the fix and a test, and open the PR, while I reviewed every step.

I learned how xarray handles a coordinate when you join only one array (`xr.concat(..., coords="different")` leaves it as a scalar, so `len()` fails), why matplotlib draws nothing for a line through one point unless you give it a marker, and how to write a test that fails before a fix and passes after it. I also learned the fork workflow end to end: `origin` and `upstream` remotes, pushing a branch to my fork, and `gh repo set-default` so the PR lands on the original repo. On the tooling side, I learned to check a repository's health with `gh api` (recent commits, who merges PRs, linked PRs) instead of trusting a label.

**Challenges Overcome**

The hardest part was environment, not code. The project only supports Linux, my tools run on Windows, and the ship-gate silently fell back to `C:\Windows` when my clone was inside WSL, so I tested that with a small script, recloned my fork on the Windows side, and kept the Python environments in WSL. I also had to catch my own and my tools' mistakes by checking facts: my shell quoting stripped every command from my memory file, the scout twice said a repo had no CONTRIBUTING file when it did, `repro-check` said my posted claim differed from my draft when it did not, and I had wrongly assumed my claim was posted from the browser until the guard log showed otherwise. In each case I fixed it by reading the real file, comment or log back, and I wrote the correction into the Toolkit blocks.

**What I'd Do Differently Next Time**

I would check the platform before choosing an issue: a Linux-only project cost me most of a day on setup that a quick look at its install notes would have flagged. I would also test a tool on a real case earlier, because two tools I trusted at first (the scout and repro-check) each gave a wrong answer on a real repo, and I would fetch live state (a comment, a file, a log) before acting on what a tool or I remembered. Finally, I would start the contribution earlier: I finished most of units 6 to 8 after the stated deadline, which left no time to wait for the maintainer's answer before writing this story.

---

## Resources Used

- [ecmwf/WeatherGenerator issue #2985](https://github.com/ecmwf/WeatherGenerator/issues/2985): the maintainer's traceback and diagnosis pointed me to `len(valid_times)` and the `xr.concat` call, so I did not have to hunt for the cause.
- The repo's `CONTRIBUTING.md` and `.github/pull_request_template.md`: they told me to open a PR against `develop`, what the checklist wants, and the lint and test commands (`scripts/actions.sh`).
- `bar_plots.py` in the same package: its "Less than two runs provided" warning, which continues instead of skipping, was the precedent for my warn-and-draw choice.
- The unit 6, 7 and 8 `INSTALL.md` files (voice guard, ship-gate, PR monitor): I followed them for setup, and their "what stops it" sections explained the stops I hit.
