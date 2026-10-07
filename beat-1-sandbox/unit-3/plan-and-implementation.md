# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**
ggovert


**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6031913507

I reproduced this on commit 2f4e82f (repro comment above). `verify_password`
raises `UnknownHashError` at `core/security.py:37` when passlib cannot identify
the stored hash format; it does not catch the exception and return `False`.

I also checked the thread's other reports: inputs like `$2b$12$abc` raise a
plain `ValueError` ("salt too small") from the same call site, not
`UnknownHashError`. My plan catches both so `verify_password` fails closed on
any unrecognizable or malformed hash, not just the format-unknown case.

My plan: wrap the `verify` call at line 37 in a try/except that catches both
`passlib.exc.UnknownHashError` and `ValueError`, returning `False` in either
case. I will also remove the `xfail` marker from
`test_verify_with_wrong_hash_format` so it becomes a passing test. I am not
touching any other auth logic, the passlib configuration, or calling code
outside `core/security.py`.

---

## Your branch

**Branch**
fix/72-verify-password-unknown-hash

**Evidence**

**Before** (unit 2 repro comment, commit 2f4e82f):

```
.venv/Scripts/python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format --runxfail -v

FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - passlib.exc.UnknownHashError: hash could not be identified
```

**After** (branch fix/72-verify-password-unknown-hash):

```
.venv/Scripts/python -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v

PASSED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format
1 passed, 1 warning in 0.98s
```

## Eval iterations

**Run history**

Run 1 (--only pkg-01,pkg-02,pkg-03): 1/3

Run 2 (--only pkg-01,pkg-02,pkg-03): 2/3 after loosening stranger-can-start pass condition

Run 3 (--only pkg-01,pkg-02,pkg-03): 2/3 still failing pkg-03 on stranger-can-start

Run 4 (--only pkg-01,pkg-02,pkg-03): 3/3 after removing repo-facts file existence check from evidence column

Run 5 (full run): 18/20 — PASS

**Package analysis**

Package: pkg-03
Gold label: accept
My rubric verdict: accept (after revision)
Agreement: yes

pkg-03 is from BurntSushi/ripgrep. The plan names crates/cli/src/decompress.rs
as the file to change and describes a one-line addition of -- before the file
path in the command builder. My rubric's stranger-can-start check initially
failed this package because the evidence column said to read the files list
"against the repo-facts block," which caused the grader to check whether the
file existed in the repo-facts block. The repo-facts block in eval bundles only
contains basic repo metadata, not a file listing, so the check failed even
though the plan clearly named a specific file and a concrete change. I revised
the evidence column to remove the repo-facts reference and added an explicit
instruction not to check file existence there. After that revision, pkg-03
flipped to accept, matching the gold label.

**Check rationale**

Quoted from rubric.md:

| stranger-can-start | The plan's files-to-touch list and approach section only |
A person who has never seen the issue could identify what to change and where
to start. Pass if the approach names at least one specific file and describes
a clear change to make there. Fail only if the approach names no files at all,
or is so vague that no starting point can be identified. Do not check whether
the file exists in the repo-facts block. | required |

This check reads that way because my first version tied the evidence to the
repo-facts block, which caused the grader to fail plans that named real files
not listed in the block's basic metadata. The pass condition focuses on whether
a stranger could start, not on whether the file can be verified from the bundle.
The explicit "Do not check whether the file exists in the repo-facts block" line
was added after pkg-03 failed on a plan that named crates/cli/src/decompress.rs
with a one-line change described clearly.

**Trade-offs**

The stranger-can-start check passes as long as the plan names at least one
specific file and describes a clear change. It does not verify that the file
actually exists in the repo. This means a plan that names a plausible but
nonexistent file (for example, core/auth.py in a repo that has no such file)
would still pass the check. I accept this miss because eval bundles do not
contain full file listings, so checking existence from the bundle is not
possible without fetching live data. In live mode the grader can verify files
against the actual repo, but the rubric must work in both modes. The trade-off
is a small risk of passing an unbuildable plan whose file list is wrong.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.


