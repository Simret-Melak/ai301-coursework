
# From an Ambiguous Bug Report to a Tested Open-Source Pull Request

## Overview

For my CodePath AI301 open-source contribution, I worked on [issue #828](https://github.com/jlab-sensing/ENTS-backend/issues/828) in the ENTS-backend repository. The issue concerned incorrect API endpoint URLs displayed after a user created a new cell. My initial investigation suggested that the reported problem had already been fixed, but a maintainer's clarification revealed a remaining defect: the application was appending a sensor ID to an endpoint that should not contain one. I reproduced the clarified bug, removed the incorrect ID from two locations in the React frontend, and added an automated regression test. After passing local tests and repository checks, I opened [pull request #881](https://github.com/jlab-sensing/ENTS-backend/pull/881). CodeRabbit completed its automated review with no actionable comments, and the PR remains open awaiting human maintainer review.

## What happened

### Selecting and investigating the issue

I began by building and improving an AI-assisted issue discovery tool called `issue-scout`. It searched GitHub issues, evaluated candidates against a rubric, and helped me identify contributions matching my skills.

My first search returned 300 issues, but the results sometimes favored recently updated issues from the same repositories. I improved the strategy by limiting repeated repository recommendations and checking whether another contributor was already working on an issue.

After additional searches and availability checks, I selected ENTS-backend issue #828, titled *Updated endpoints when creating new cells*. The task appeared manageable and involved debugging API endpoint references.

The relevant component was:

`frontend/src/pages/profile/components/AddCellModal.jsx`

The issue said the success screen displayed outdated Power and TEROS endpoint paths and requested that they use `/api/sensor/`.

### My first reproduction did not find the reported bug

I inspected the component and its Git history before changing any code.

I discovered that an earlier merged commit, `eb634be`, had already replaced the old `/api/power/` and `/api/teros/` paths with `/api/sensor/`.

I created a Vitest component test to render the cell-creation success screen. The test confirmed that the old endpoint paths were absent.

Based on the literal issue description, I recorded the result as **NOT REPRODUCED** rather than claiming that I had found a bug.

I documented my evidence and [asked the maintainer whether another scenario remained](https://github.com/jlab-sensing/ENTS-backend/issues/828#issuecomment-6924870574).

### Maintainer feedback changed my understanding

On November 17, 2026, maintainer `jmadden173` clarified that the endpoint should be:

`/api/sensor/`

The important detail was that it must contain **no sensor ID**.

[Maintainer clarification](https://github.com/jlab-sensing/ENTS-backend/issues/828#issuecomment-6963665152)

This revealed the problem I had initially missed. Although the endpoint path was correct, the success screen still appended the newly created cell's ID.

For example, when the mocked cell had ID `42`, the application displayed:

```text
https://dirtviz.jlab.ucsc.edu/api/sensor/42
```

The expected URL was:

```text
https://dirtviz.jlab.ucsc.edu/api/sensor/
```

I updated my reproduction criteria to match the clarified requirement and confirmed that both the Power Data and TEROS Data rows contained the unwanted suffix.

The maintainer's response changed my work from investigating a potentially resolved issue to implementing a specific, reproducible correction.

### Implementing the fix

I created the branch `fix/828-sensor-endpoints` from upstream commit `13413f2`.

The problem was limited to two displayed endpoint strings in `AddCellModal.jsx`, at lines 442 and 465.

My implementation removed the `{response.id}` interpolation from both locations.

**Evidence 1 — Actual code diff from commit `1a92673`:**

```diff
- https://dirtviz.jlab.ucsc.edu/api/sensor/{response.id}
+ https://dirtviz.jlab.ucsc.edu/api/sensor/
```

This exact change was applied to both the Power Data and TEROS Data rows.

I intentionally avoided modifying backend routes or unrelated formatting. The final commit contained two changed files: the frontend component and one new 70-line regression test.

### Testing the correction

I added `frontend/src/__tests__/AddCellModal.test.jsx` to verify that the success screen displayed the correct endpoint.

The test mocked the cell-creation service with this response:

```javascript
{
  id: 42,
  name: 'Test Cell'
}
```

It then checked that both rendered endpoint URLs ended in `/api/sensor/`, contained no appended numeric ID, and did not use the old Power or TEROS paths.

To prove the test detected the original defect, I ran the same committed regression test against the original upstream code in an isolated Git worktree.

**Evidence 2 — Before-and-after regression test results:**

```text
BEFORE FIX — upstream/main (13413f2)

AssertionError:
expected 'https://dirtviz.jlab.ucsc.edu/api/sen…'
to match /\/api\/sensor\/$/

Test Files  1 failed (1)
Tests       1 failed (1)


AFTER FIX — commit 1a92673

Test Files  1 passed (1)
Tests       1 passed (1)
```

The test failed on the original code because the URLs included `/42`. After the fix, both endpoints matched the required URL.

I also ran the complete frontend test suite.

**Evidence 3 — Full test results:**

```text
$ cd frontend && npx vitest run

Test Files  37 passed (37)
Tests       266 passed (266)
```

The repository's frontend lint command, `npm run lint`, and coverage command, `npm run coverage`, also completed successfully.

These results gave me confidence that the specific defect was corrected without breaking the existing frontend tests.

### Opening the pull request

Before opening the PR, I installed and configured the Unit 7 ship-gate. I created a manifest using the repository's actual CI commands and ran the required checks.

The ship-gate passed, including the frontend lint and coverage commands and the `pr-precheck` checks.

I then pushed my branch and opened [PR #881](https://github.com/jlab-sensing/ENTS-backend/pull/881), titled *fix(frontend): remove sensor ID from cell creation endpoints*.

The PR included the focused code change, regression test, testing evidence, limitations, and a reference to issue #828.

CodeRabbit subsequently completed its automated review. Its reported pre-merge checks passed, it identified no actionable comments, and it rated the merge risk as minimal.

This was a useful milestone, but it was not human approval. At the last verified check, the PR was open, mergeable, and awaiting maintainer review.

### Learning to respond only when necessary

During Unit 8, I installed a PR monitor and wrote an evidence-based communication playbook.

I investigated five recently merged external-contributor PRs and used their response times to establish a 14-day threshold for an initial review nudge.

When I ran the monitor on PR #881, it classified the thread as `FEEDBACK-IN` because CodeRabbit had commented.

However, the generated draft correctly recognized that the automated review contained no actionable feedback.

Its recommendation was:

```text
MOVE: no action — hold, nothing to answer
```

I reviewed that recommendation and chose not to post an unnecessary comment. This showed me that responsible AI-assisted workflows require judgment, not just automation.

## Limitations and what's next

My testing had one important limitation: I could not complete a full browser end-to-end test because the local application required Google OAuth credentials that were unavailable in my development environment.

Instead, I used a Vitest component test that rendered the actual success-screen behavior. This provided direct evidence for the endpoint correction, but it did not replace complete browser testing.

The pull request also remains dependent on human maintainer review. Passing local checks and receiving a successful automated review do not guarantee that a contribution will be merged.

If a maintainer requests changes, my next step will be to review each comment, update the implementation or tests where necessary, rerun the required checks, and request another review.

For future contributions, I would clarify ambiguous acceptance criteria earlier and create a failing regression test before implementing a fix. I would also continue using evidence-based communication rules to avoid unnecessary follow-ups.

The most important outcome of this project was learning to move from an uncertain bug report to a reproducible problem, a focused implementation, and an evidence-backed pull request. It demonstrated how testing, maintainer communication, and careful use of AI-assisted tools can work together in a real open-source contribution.
