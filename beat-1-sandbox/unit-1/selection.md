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
 
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36
 
**Verdict output**
 
```
Ranked read-out (all three accepted)
 
1. Issue #3 — Add a content hash to skip re-embedding unchanged documents (best fit)
Bounded to the ingestion subsystem (ingestion/pipeline.py + core/models/ingested_source.py). Pure Python, and it works directly on the embedding pipeline — reducing embedding API calls is the most direct "integrating AI into software" match to your stated goals. It's the most involved of the three (tier-2, 4–6h) and carries no beginner label, so it's a stretch-but-aligned pick.
 
2. Issue #36 — Add a test for POST /reviews when the profile has no ingested docs (gentlest on-ramp)
Single Python test file (tests/unit/test_review_routes.py), tier-1, and the only candidate carrying the good first issue label (passes the preferred check). Python practice, though test coverage rather than AI-integration work.
 
3. Issue #67 — Review creation does not verify profile ownership (least aligned)
Bounded Python bug fix in one file (core/services/review_service.py). Solid Python, but it's an auth/ownership fix with no AI-integration angle and no beginner label.
 
Per-check grades (identical required-check results across all three; they differ only on the preferred beginner-label check):
 
┌────────────────────────────┬──────┬──────┬──────┐
│           Check            │  #3  │ #36  │ #67  │
├────────────────────────────┼──────┼──────┼──────┤
│ Maintainer alive           │ pass │ pass │ pass │
├────────────────────────────┼──────┼──────┼──────┤
│ Repo in use                │ pass │ pass │ pass │
├────────────────────────────┼──────┼──────┼──────┤
│ Scope fits a newcomer      │ pass │ pass │ pass │
├────────────────────────────┼──────┼──────┼──────┤
│ Nobody else is on it       │ pass │ pass │ pass │
├────────────────────────────┼──────┼──────┼──────┤
│ Not a claim graveyard      │ pass │ pass │ pass │
├────────────────────────────┼──────┼──────┼──────┤
│ Repo accepts AI            │ pass │ pass │ pass │
├────────────────────────────┼──────┼──────┼──────┤
│ Beginner label (preferred) │ fail │ pass │ fail │
└────────────────────────────┴──────┴──────┴──────┘
 
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/3",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Default branch commit Sep 16 2026 (12 days before today); opener Aburke225 also opened the issue Sep 10 and commits to the repo"},
      {"name": "Repo in use", "grade": "pass", "evidence": "Latest default-branch commit Sep 16 2026, within 30 days"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "One coherent feature bounded to the ingestion subsystem: ingestion/pipeline.py + core/models/ingested_source.py"},
      {"name": "Nobody else is on it", "grade": "pass", "evidence": "No assignees, no comments, no linked PRs"},
      {"name": "Not a claim graveyard", "grade": "pass", "evidence": "Zero claim/abandon cycles (no comments)"},
      {"name": "Repo accepts AI", "grade": "pass", "evidence": "docs/CONTRIBUTING.md is silent on AI-assisted contributions"},
      {"name": "Beginner label", "grade": "fail", "evidence": "Labels are tier-2/enhancement/ingestion/docs/devops — no good-first-issue/beginner/starter/help-wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Default branch commit Sep 16 2026 (12 days before today); opener Aburke225 opened the issue Sep 10 and commits to the repo"},
      {"name": "Repo in use", "grade": "pass", "evidence": "Latest default-branch commit Sep 16 2026, within 30 days"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single bounded task in one file: tests/unit/test_review_routes.py"},
      {"name": "Nobody else is on it", "grade": "pass", "evidence": "No assignees, no comments, no linked PRs"},
      {"name": "Not a claim graveyard", "grade": "pass", "evidence": "Zero claim/abandon cycles (no comments)"},
      {"name": "Repo accepts AI", "grade": "pass", "evidence": "docs/CONTRIBUTING.md is silent on AI-assisted contributions"},
      {"name": "Beginner label", "grade": "pass", "evidence": "Carries 'good first issue' and 'tier-1' labels"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/67",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "Default branch commit Sep 16 2026 (12 days before today); opener Aburke225 opened the issue Sep 10 and commits to the repo"},
      {"name": "Repo in use", "grade": "pass", "evidence": "Latest default-branch commit Sep 16 2026, within 30 days"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Bounded bug fix in one file: core/services/review_service.py"},
      {"name": "Nobody else is on it", "grade": "pass", "evidence": "No assignees, no comments, no linked PRs"},
      {"name": "Not a claim graveyard", "grade": "pass", "evidence": "Zero claim/abandon cycles (no comments)"},
      {"name": "Repo accepts AI", "grade": "pass", "evidence": "docs/CONTRIBUTING.md is silent on AI-assisted contributions"},
      {"name": "Beginner label", "grade": "fail", "evidence": "Labels are tier-2/bug — no good-first-issue/beginner/starter/help-wanted"}
    ],
    "verdict": "accept"
  }
]
```
 
---
 
## Eval iterations
 
Quote source text directly in each field below. Paraphrase does not satisfy them.
 
**Run history**
 
Run 1: 12/20 scored items agreed.
Run 2 (final, committed): 18/20 scored items agreed (bar: 18/20: PASS). Category floor cleared in every category: claimed 4/4, clear-accept 6/8, dead-repo 3/3, policy 1/1, scope 4/4.
 
**Issue analysis**
 
issue-01 (source: conda/conda#16475). Gold label: accept. My rubric's verdict: reject, failing "Scope fits a newcomer." The issue asks for a documentation change spanning five files (a new task page plus updates to manage-pkgs.rst, pip-interoperability.rst, new-features.md, and optionally troubleshooting.rst). My check's pass condition allows documentation changes across "any number of files, each edit small and independent," which I intended to cover exactly this case, but the grading model still read the five-file spread as failing scope. My rubric treats multi-file spread as a red flag by default, and my attempted carve-out for documentation didn't fully overcome that default for this specific issue.
 
**Check rationale**
 
"Scope fits a newcomer | Issue body; comment thread | The issue describes one coherent task within a single subsystem — either (a) a documentation change (any number of files, each edit small and independent), or (b) a code change bounded to one file or one clearly-related area of the codebase (several similar, related fixes within the same subsystem still count as bounded) | required"
 
I wrote this check because my first version only allowed single-file changes, which incorrectly rejected multi-file documentation tasks and multi-part bug fixes that were actually all one coherent problem (e.g. a UI freeze with several related causes and candidate fixes in one subsystem). The revised wording tries to separate "spans several files because it's inherently risky/interconnected" from "spans several files because the same idea needs to be written down in a few places," since only the first is a real risk for a newcomer.
 
**Trade-offs**
 
This check still misses some multi-file documentation issues (issue-01), meaning my rubric is more conservative on scope than I intended — it will sometimes reject well-scoped docs work that a human reviewer would accept. I re-ran issue-01 and issue-19 with --only after this revision and confirmed they still fail; I chose not to loosen the wording further because doing so risks accepting genuinely risky multi-file code refactors, which is a worse failure mode than rejecting a few good documentation issues.
 
---
 
## Selection rationale
 
Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.
 
**Selection rationale**
 
1. Fit: I'm comfortable with Python and wanted a bounded, low-risk first contribution rather than stretching into unfamiliar territory right away. Issue #36 is a single test file with a clear, narrow scope (2-3 hours), which matches where I am right now more than a bigger pipeline change would.
2. What the verdict caught vs. what I weighed myself: the rubric correctly confirmed all the required signals (active maintainer, active repo, bounded scope, nobody else on it, no claim history, AI-friendly policy). What it couldn't weigh was my own comfort level as a first-time contributor — it ranked issue #3 higher because it better matches my stated interest in AI-integration work, but I judged that starting with the safer, smaller issue (#36) is the better sequencing for an actual first contribution, and I can pursue the more ambitious one later.
3. Anticipated difficulty claiming it: low. The issue has no assignee, no comments, and no linked PRs, so there's no ambiguity about whether it's available. The main risk is making sure I correctly understand the existing test file's conventions before adding a new test case.
---
 
Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
 