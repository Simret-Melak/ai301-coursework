
# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

Simret-Melak

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36#issuecomment-6180322160

Following up on my reproduction above: the endpoint doesn't crash on a
profile with no ingested documents, but it also doesn't return an
error — it silently completes with a fabricated score and feedback
based on hardcoded placeholder content.

Picking this up alongside @Kunalkrk's proposed 422 validation above —
my plan is to add `tests/unit/test_review_routes.py` (this file didn't
exist yet) with a test asserting `POST /reviews` returns a 422 for a
profile with no ingested sources, marked `xfail(strict=True)` per the
repo's documented seeded-bug convention, since that behavior doesn't
exist yet. This keeps the test and the actual validation fix as
separate, reviewable pieces rather than bundling them.

I'll build the test against Kunalkrk's proposed status code; happy to
adjust if a different error code is preferred. Will report back once
it's built and confirmed failing correctly (strict xfail) against the
current code.

---

## Your branch

**Branch**

`fix/36-review-empty-profile-test`

**Evidence**

### Before — Unit 2 reproduction

Reproduction comment: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/36#issuecomment-5984300776

Environment: macOS (Apple Silicon), Python 3.14.8, Docker Desktop 28.3.0 with PostgreSQL 16 (host port 5434), Redis 7, and ChromaDB 0.4.22.

Project setup and startup commands recorded in Unit 2:

```bash
make setup
make run
```

API reproduction steps recorded in Unit 2 (the original report described HTTP requests rather than supplying literal `curl` commands):

1. Log in as the seeded test user (`user1@example.com`) using `POST /auth/login`.
2. Create a profile with no GitHub username, resume, or portfolio URL using `POST /profiles`, with those form fields empty.
3. Confirm that the created profile has no sources:

```json
{
  "id": "74b16c45-189b-48a2-a99c-607d6d8e555b",
  "github_username": null,
  "portfolio_url": null,
  "resume_filename": null
}
```

4. Submit a review using `POST /reviews` with this request body:

```json
{"profile_id": "74b16c45-189b-48a2-a99c-607d6d8e555b"}
```

5. Observe these backend logs, copied from the Unit 2 reproduction report:

```text
2026-10-04 16:04:17 [info] review_processing_started      profile_id=74b16c45-189b-48a2-a99c-607d6d8e555b review_id=0752e928-8004-47c8-aade-f4321f65c0c9
2026-10-04 16:04:17 [info] ingestion_pipeline_completed   review_id=0752e928-8004-47c8-aade-f4321f65c0c9 sources_count=0
2026-10-04 16:04:17 [info] agent_orchestration_completed  review_id=0752e928-8004-47c8-aade-f4321f65c0c9 sections_count=2
2026-10-04 16:04:17 [info] rag_retrieval_completed        review_id=0752e928-8004-47c8-aade-f4321f65c0c9
2026-10-04 16:04:17 [info] safety_checks_passed
2026-10-04 16:04:17 [info] review_processing_completed    overall_score=0.81 review_id=0752e928-8004-47c8-aade-f4321f65c0c9
```

**Before result:** The ingestion pipeline reported `sources_count=0`, yet the background review completed with a score of `0.81` instead of stopping with a validation error. No test previously covered this case in `tests/unit/test_review_routes.py`.

### After — Unit 3 change

I added the planned expected-failure unit test on branch `fix/36-review-empty-profile-test` in commit `714e778` (`test: add xfail test for POST /reviews with no ingested documents (issue #36)`). The change adds test coverage for the proposed HTTP 422 behavior without implementing the 422 validation itself.

Command executed from the PathReview repository:

```bash
pytest tests/unit/test_review_routes.py -v
```

Relevant output from the October 23 test run:

```text
tests/unit/test_review_routes.py::TestReviewRoutes::test_create_review_for_profile_with_no_ingested_documents_returns_422 XFAIL (issu...) [100%]

=============================================================== warnings summary ================================================================
core/config.py:7
  /Users/simretmelak/Desktop/Codepath/pathreview-ai301-fa26-s1/core/config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
========================================================= 1 xfailed, 1 warning in 0.46s =========================================================
```

**After result:** The new test is discovered and marked `XFAIL` as planned; the intended 422 behavior remains unimplemented. This is a regression-coverage change rather than proof of a fixed endpoint. The Pydantic warning is unrelated to Issue #36. The original Unit 2 HTTP-request sequence was not re-run after this test-only change; the after evidence is the new unit test's execution, rather than a new end-to-end response.

---

## Eval iterations

**Run history**

**Attempt 1 — unscored execution failure.** The first supplied full-run attempt could not produce verdicts because Claude Code exited with status 1 for every package. The output reported:

```text
20 item(s) errored; fix and re-run.
agreement: 0/0 scored items
partial run: NOT written to eval-run.txt
```

Troubleshooting showed Claude Code was not logged in (`Not logged in · Please run /login`); after `/login`, Claude Code responded to a test prompt. This attempt had no valid agreement score and did not overwrite `eval-run.txt`.

**Attempt 2 — 19/20 agreement (PASS).** After authentication was restored, I ran:

```bash
cd ~/Desktop/Codepath/ai301-unit3-starter/eval
python3 run_eval.py --rubric ~/.claude/skills/plan-check/rubric.md --evidence ~/.claude/skills/plan-check/references/evidence-guide.md --save-run eval-run.txt
```

The output was:

```text
categories: clear-accept 6/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4
agreement: 19/20 scored items  (bar: 18/20: PASS)
run written to eval-run.txt
```

This is the final valid scored run shown in my records and matches the `eval-run.txt` to be uploaded. Every category met the category floor.

**Package analysis**

I selected **`pkg-14`** (category: `clear-accept`). The instructor's gold label was **`accept`**, but my rubric's verdict was **`reject`**. The evaluation output stated:

```text
pkg-14  clear-accept       accept  reject   NO     failed: Scope is bounded, Plan is executable by a stranger
```

My rubric treats explicit scope boundaries and independently executable steps as mandatory. The `Scope is bounded` check requires specific files or functions and an explicit account of what will *not* change; the `Plan is executable by a stranger` check requires that another contributor could begin the work without clarification. The grader found these requirements unmet for `pkg-14`, so its `reject` verdict followed from my all-required-checks rule. The gold `accept` label shows that these requirements were too strict for this acceptable package. The output does not isolate which one check would independently have changed the verdict; both failed.

**Check rationale**

The following row is quoted exactly from my final `rubric.md`:

```text
| Scope is bounded | The plan's scope statement and list of files to touch | The plan names specific files/functions it will change and explicitly states what it will NOT touch; it is not an open-ended rewrite or a vague "clean up the code" | required |
```

I chose this wording over a looser requirement to merely identify a general area of work. Naming specific files or functions makes the proposal actionable, and naming exclusions constrains scope creep before implementation. I made the check `required` because a vague or expanding scope can undermine a plan even if its diagnosis is correct. In my own Issue #36 plan I limited the work to the new test file and explicitly excluded implementing the 422 validation and modifying the placeholder orchestration and RAG functions.

**Trade-offs**

The explicit-exclusions requirement makes the rubric more conservative: it can reject a bounded, workable plan that communicates its limits implicitly rather than listing what it will not change. `pkg-14` illustrates that cost; the gold label was `accept`, while my rubric rejected it in part on `Scope is bounded` (and also `Plan is executable by a stranger`). I retained the check because the final scored run achieved 19/20 agreement, including **4/4 scope-creep** and **3/3 unbuildable** matches. Those results support keeping strong scope and executability gates, even though the rule may wrongly hold a borderline acceptable plan.
