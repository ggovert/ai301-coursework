# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

ggovert

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5904512689

I'd like to investigate this as a first contribution. The issue is that `verify_password` in `core/security.py` lets `UnknownHashError` escape when the stored hash is malformed, instead of failing closed and returning `False`.

My next steps are setting up the environment from `docs/SETUP.md`, reading `core/security.py` to locate where `UnknownHashError` escapes instead of `verify_password` returning `False`, and running the existing xfail test to see what it actually does. I'll post my findings and a repro report here before opening a PR.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5905184781

Result: reproduced. `verify_password` raises `UnknownHashError` instead of returning `False` when passed a malformed stored hash.

Environment: Python 3.14.7 (CI target is 3.11), pytest 9.1.1, passlib 1.7.4, bcrypt 4.3.0, Windows 11 (x86_64). Repo commit: 2f4e82f.

Steps:

1. Cloned fork, ran `make setup` from `docs/SETUP.md` with Docker services running.
2. Ran the xfail test with the marker suppressed:

`.venv/Scripts/python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail -v`

Output:

`FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - passlib.exc.UnknownHashError: hash could not be identified`

Traceback frames: `core/security.py:37` verify_password → `passlib/context.py:2343` verify → `passlib/context.py:2031` _get_or_identify_record → `passlib/context.py:1132` identify_record raises `UnknownHashError("hash could not be identified")`.

Expected: `verify_password` returns `False` when the stored hash is not a recognizable format.

Actual: `passlib.exc.UnknownHashError: hash could not be identified` propagates uncaught from `core/security.py:37`.

---

## Eval iterations

**Run history**

Run 1: 3/3 (limit run, smoke test)
Run 2: 17/20 — category floor unmet: no match in disclosure
Run 3: 17/20 (full run with encoding fix) — category floor unmet: no match in disclosure
Run 4 (--only pkg-09,pkg-10,pkg-20): 3/3 after fixing behavior check and adding AI disclosure check
Run 5 (--only pkg-03,pkg-05,pkg-12,pkg-20): 3/4 — pkg-05 still failing Steps are followable
Run 6 (--only pkg-05,pkg-08,pkg-12): 3/3 after loosening steps check
Run 7 (full run): 20/20 — PASS

**Package analysis**

Package pkg-20 (gold: reject, my rubric: reject, agreement: yes).

pkg-20 is from ghostty-org/ghostty, whose `AI_POLICY.md` requires disclosure of any AI use in any form for comments to maintainers. The claim and repro comments in the bundle contain no disclosure statement. My rubric's "AI disclosure" check reads: "If the repo requires disclosure for issue comments, the comment includes a statement naming the tool and extent of use; if the policy explicitly states no disclosure is required for issue comments, this check passes." The check failed because the policy is explicit and broad -- it covers all comments -- and neither comment included a disclosure line. My rubric initially missed this package entirely because I had no separate disclosure check; it was bundled inside "Conventions followed," which was too broad for the grader to isolate. Splitting it into its own check fixed the miss.

**Check rationale**

Quoted from `rubric.md`:

> | AI disclosure | The repo-facts block read for any AI-use disclosure policy in CONTRIBUTING.md or a dedicated AI policy file | If the repo requires disclosure for issue comments, the comment includes a statement naming the tool and extent of use; if the policy explicitly states no disclosure is required for issue comments, this check passes | required |

This check exists as a separate row because bundling disclosure into "Conventions followed" caused the grader to miss pkg-20. The original "Conventions followed" check covered template structure and disclosure together, but the grader did not focus on disclosure specifically when multiple conditions were in one cell. Splitting it into its own check with a single focused pass condition fixed the miss and cleared the category floor.

**Trade-offs**

The "AI disclosure" check passes automatically when the repo's policy says nothing about issue comments. This means a repo with a PR-only AI policy and a repo with no policy at all are treated the same -- both pass. The trade-off is that a repo with an ambiguous policy (one that applies to "contributions" without defining whether comments are contributions) will also pass, even if a maintainer would read it as requiring disclosure. I accept this miss because the alternative -- failing any ambiguous policy -- would cause false rejects on packages where no disclosure is actually required. pkg-05 (conda) is an example: its policy applies only to pull requests, and treating it as requiring comment disclosure caused a false reject that I had to fix by loosening the check.
