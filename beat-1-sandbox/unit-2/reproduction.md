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

Simret-Melak

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36#issuecomment-5973738479

Hi! I'd like to work on this issue as my first contribution to this project.

My plan is to add a test case to `tests/unit/test_review_routes.py`
covering `POST /reviews` when the target profile has no ingested
documents, since that path doesn't currently appear to have coverage.

I'll set up the project environment, confirm the current (missing or
incorrect) behavior, and report back here with what I find before
opening a PR.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36#issuecomment-5984300776

**Reproduction report**

**Environment:**
- macOS (Apple Silicon)
- Python 3.14.8, installed via python.org installer, used through a
  local virtualenv created by the project's Makefile
- Docker Desktop 28.3.0 running Postgres 16 (port 5434, remapped from
  the default 5433 due to a local port conflict), Redis 7, and
  ChromaDB 0.4.22
- Set up from a fresh clone via `make setup` and started via `make run`
- Backend: http://localhost:8000, Frontend: http://localhost:5173

**Steps:**
1. Logged in as a seeded test user via `POST /auth/login`
   (user1@example.com)
2. Created a new profile with no GitHub username, no resume, and no
   portfolio URL via `POST /profiles` (multipart form, all three
   fields left empty)
3. Confirmed the created profile has no sources attached:
   ```json
   {
     "id": "74b16c45-189b-48a2-a99c-607d6d8e555b",
     "github_username": null,
     "portfolio_url": null,
     "resume_filename": null
   }
   ```
4. Created a review for that profile via `POST /reviews` with
   `{"profile_id": "74b16c45-189b-48a2-a99c-607d6d8e555b"}`
5. Observed the backend's background processing logs for that review

**Observed behavior:**
```
2026-10-04 16:04:17 [info] review_processing_started      profile_id=74b16c45-189b-48a2-a99c-607d6d8e555b review_id=0752e928-8004-47c8-aade-f4321f65c0c9
2026-10-04 16:04:17 [info] ingestion_pipeline_completed   review_id=0752e928-8004-47c8-aade-f4321f65c0c9 sources_count=0
2026-10-04 16:04:17 [info] agent_orchestration_completed  review_id=0752e928-8004-47c8-aade-f4321f65c0c9 sections_count=2
2026-10-04 16:04:17 [info] rag_retrieval_completed        review_id=0752e928-8004-47c8-aade-f4321f65c0c9
2026-10-04 16:04:17 [info] safety_checks_passed
2026-10-04 16:04:17 [info] review_processing_completed    overall_score=0.81 review_id=0752e928-8004-47c8-aade-f4321f65c0c9
```

The ingestion pipeline correctly detects `sources_count=0`, confirming
the profile has nothing to ingest. Despite this, the review does not
error, warn, or halt. It proceeds through agent orchestration and RAG
generation (which return hardcoded placeholder content regardless of
input) and completes successfully with `status="complete"` and
`overall_score=0.81`, along with specific-sounding fabricated feedback
(e.g. "Add more detail on AI/ML experience," confidence 0.85) for a
profile that submitted no actual data.

**Conclusion:**
Issue #36 does not crash. However, it also does not "return an
appropriate error," as the issue requests — instead, it silently
fabricates a confident, specific-looking review for a profile with no
real content. I'd consider this the more concerning of the two
documented behaviors (crash vs. silent fake success), since a crash is
at least visibly broken, whereas this failure mode could mislead a
real user into trusting feedback that isn't based on their actual
portfolio.

---

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1: 12/20 scored items agreed.
Run 2 (final, committed): 18/20 scored items agreed (bar: 18/20: PASS). Category floor cleared in every category: clear-accept 6/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4.

**Package analysis**

pkg-20 (source: ghostty-org/ghostty#13604). Gold label: reject. My rubric's initial verdict: accept, incorrectly. The repo's AI_POLICY.md requires that "all AI usage in any form must be disclosed," but the candidate claim and repro report never mention AI at all. My original "Words respect repo conventions" check only flagged a disclosure problem if AI use was detected and not disclosed — since the comment never mentions AI either way, the check read that as "nothing to disclose" and passed it. After revising the check to state explicitly that silence does not satisfy a mandatory-disclosure policy, the rubric correctly rejects this package.

**Check rationale**

"Words respect repo conventions | The claim/repro comment text; the repo's contribution/AI policy | If the repo's policy requires disclosing AI use, the comment must contain an explicit disclosure statement (naming the tool and extent of assistance) — silence on AI use does not satisfy a mandatory-disclosure policy. The comment also does not promise a fix or a date, and breaks no rule in voice-guide.md | required"

I revised this check after pkg-20 revealed that my original wording let a mandatory-disclosure policy be satisfied by silence. The addition of "silence on AI use does not satisfy a mandatory-disclosure policy" closes that gap directly, rather than relying on the grading model to infer it.

**Trade-offs**

Tightening this check to catch pkg-20 changed two other packages' results: pkg-07 and pkg-10, which had previously agreed with gold, flipped to disagree after the revision (19/20 → 18/20 overall). I re-ran both with `--only` to confirm the flip was real and not a fluke, and chose to accept the trade-off rather than loosen the wording again, since passing the disclosure category floor was the higher priority and the two new misses are in different, already-covered categories (clear-accept).

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.