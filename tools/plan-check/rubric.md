# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis matches evidence | The plan's stated cause, read against the repro evidence's observed behavior | The diagnosis names a cause that is directly supported by what the repro evidence actually showed, not a plausible-sounding guess the evidence doesn't confirm | required |
| Scope is bounded | The plan's scope statement and list of files to touch | The plan names specific files/functions it will change and explicitly states what it will NOT touch; it is not an open-ended rewrite or a vague "clean up the code" | required |
| Fix targets the cause, not the symptom | The plan's approach, read against the diagnosis | The described change addresses the root cause identified in the diagnosis, not just a surface symptom that would leave the underlying cause unfixed | required |
| Plan is executable by a stranger | The plan's approach and file list | A contributor unfamiliar with the plan's author could start making the described changes without needing to ask what a step means | required |
| Test plan is observable | The plan's test plan section | The test plan describes a concrete, observable before/after check (e.g. "currently returns X, after the fix should return Y"), not just "test that it works" | required |
| Unknowns are disclosed, not hidden | The plan's risks/unknowns section, read against the rest of the plan | Any genuine uncertainty (edge cases not covered, assumptions made) is explicitly named as uncertain, not written with false confidence | required |
| Comment respects thread and conventions | The plan comment text, read against the issue thread and the repo's stated conventions/policy | The comment reflects the actual thread (doesn't ignore existing discussion or contradict it) and follows the repo's contribution conventions (including AI-disclosure if required) | required |

## Verdict rule

Accept (ready) if every `required` check passes. If any `required` check
fails, reject (hold).

`unclear` counts as fail for `required` checks: if there isn't enough
evidence to confirm a plan is sound, it doesn't go forward. There are no
`preferred` checks in this rubric; all seven failure families named in
lecture are treated as required, since a plan weak in any one of them is
genuinely not ready to build from.
