## Diagnosis and grounding

Where it lives: in an eval bundle, the plan's "Diagnosis" or "Cause"
heading, read against the repro-evidence block (the Unit-2-style
environment/steps/observed-behavior section). In live mode, the
student's draft plan.md's diagnosis section, read against their
posted Unit 2 repro comment.

What good looks like: the stated cause directly explains the specific
behavior the repro evidence recorded — not a plausible-sounding
general explanation that the evidence doesn't actually pin down. A
diagnosis that could be written without ever having read the repro
evidence (e.g. "the code probably doesn't handle edge cases") fails
this; one that cites the exact observed symptom (e.g. "the ingestion
pipeline returns an empty list but downstream steps never check for
this, so they proceed on hardcoded placeholder data") passes.

## Scope

Where it lives: the plan's "Scope" section, specifically an in-scope
statement and an explicit not-in-scope or "will not touch" line, plus
the "Files" list naming concrete files or functions.

What good looks like: one bounded, specific change — named files, a
describable single fix — rather than an open-ended rewrite, a
"clean up while I'm in there" addendum, or a scope that could
reasonably balloon into touching unrelated code. A good scope line
reads like "add validation in review_service.py's process_review
function," not "improve the review pipeline's robustness."

## Executability

Where it lives: the plan's "Approach" section and its file list,
read as a sequence of concrete actions.

What good looks like: a contributor unfamiliar with this specific
plan's author could read the approach and start making the described
changes without needing to ask what a step means or where something
is. Vague verbs ("handle the case better," "improve the check") fail
this; specific ones ("add an early return with HTTP 400 when
ingestion_results is empty, before calling _run_agent_orchestration")
pass.

## Test plan

Where it lives: the plan's "Test plan" section, read against the
repro evidence's own steps and observed artifacts.

What good looks like: the test plan names a concrete current value and
an expected new value, mapped onto the same steps used in the Unit 2
repro (e.g. "currently: POST /reviews on an empty profile returns
status=complete with a fabricated score; after the fix: the same
request should return a 4xx error before processing begins"). A vague
test plan ("test that it works correctly now") fails, regardless of
how much other detail surrounds it.

## Honesty

Where it lives: the plan's "Risks and unknowns" section, and (after
the build) the "Deviations" section at the bottom of plan.md.

What good looks like: genuine uncertainty is named explicitly as
uncertain ("I'm not sure whether other endpoints have the same gap"),
rather than omitted or written with false confidence. A plan with no
risks section at all, for a change with real open questions, reads as
overconfident. After the build, a filled "Deviations" section (even
one stating plainly that nothing changed) is the honest record of
what actually happened versus what was planned.

## Comms

Where it lives: the plan comment text (draft or posted), read against
the issue thread's prior comments (including the student's own Unit 2
claim and repro comments) and the repo-facts block's stated
contribution policy, including any AI-use disclosure requirement.

What good looks like: the comment engages with the actual thread (it
doesn't repeat information already established, and it doesn't
contradict anything a maintainer said) and follows the repo's actual
conventions, including disclosing AI assistance if the policy requires
it. A comment that could be posted on any plan for any issue, with no
reference to this thread's specifics, fails this.