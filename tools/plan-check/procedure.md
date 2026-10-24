## Read order

1. Read the issue thread first (title, body, comments) and note: the
   exact bug being reported, and anything a maintainer already said
   about expected scope or approach.
2. Read the repro evidence next (the Unit 2-style reproduction: steps,
   environment, observed behavior). Note the specific, concrete cause
   the evidence actually demonstrates, in the executor's own words,
   separate from whatever the plan claims.
3. Read the plan itself last (diagnosis, scope, files, approach, test
   plan, risks). Reading it last ensures the executor's understanding
   of "what the evidence shows" isn't anchored by the plan's own
   framing of it.
4. Read the plan comment (if present) and the repo's stated
   conventions/AI policy last of all, since those are evaluated
   independently of whether the plan itself is technically sound.

## Evidence gathering

1. For **Diagnosis matches evidence**: pull the plan's stated cause
   (usually under a "Diagnosis" or "Cause" heading) and the repro
   evidence's observed behavior (usually a log excerpt or described
   symptom). Record both as short quotes.
2. For **Scope is bounded**: pull the plan's list of files/functions
   to change, and any explicit "will not touch" statement. Record the
   file list verbatim.
3. For **Fix targets the cause, not the symptom**: pull the plan's
   "Approach" section and compare it against the cause recorded in
   step 1. Record whether the approach's described change sits at the
   same layer/location as the cause, or somewhere downstream of it.
4. For **Plan is executable by a stranger**: read the approach section
   as if the executor has never seen the codebase. Record any step
   that requires unstated context to act on.
5. For **Test plan is observable**: pull the plan's "Test plan"
   section. Record whether it states a concrete before-value and
   after-value, or only a vague intention.
6. For **Unknowns disclosed**: pull the plan's "Risks/Unknowns"
   section. Record whether it exists and whether it names anything
   genuinely uncertain about the approach.
7. For **Comment respects thread and conventions**: pull the plan
   comment text, the repo's contribution/AI policy (from the
   repo-facts block or references/evidence-guide.md), and the thread
   highlights. Record any contradiction or ignored prior discussion.

## Check execution

1. Execute checks in the same order as the table in rubric.md, top to
   bottom.
2. Grade each check using only the evidence recorded for that check in
   Evidence gathering; do not re-read the full package per check.
3. If the evidence for a check is genuinely absent (the plan has no
   test-plan section at all, for example), grade that check `unclear`,
   not a guessed pass or fail.
4. Write one line of reasoning per check, naming the specific evidence
   quote that produced the grade.

## Verdict assembly

1. Apply rubric.md's verdict rule: accept only if every required check
   passed; any required fail or required unclear (treated as fail)
   means reject.
2. In the output, quote the single check that most directly decided
   the verdict (the first required check, in table order, that failed
   or was unclear; if all passed, quote the check the executor judged
   most load-bearing for this package).
3. State the final verdict as `accept` or `reject`, matching the JSON
   block's `verdict` field exactly.