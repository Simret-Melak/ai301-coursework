# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

# Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment is recorded | The repro report's environment section (OS, language/runtime version, dependency versions, install commands actually run) | A stranger could set up an equivalent environment from what's written, without guessing at versions or missing install steps | required |
| Steps are complete and followable | The repro report's step-by-step section | Every step needed to go from a clean checkout to triggering the behavior is present, in order, with no unstated assumptions or skipped setup | required |
| Behavior shown matches the issue | The artifacts (output/error excerpts, screenshots, logs) read against the issue's own description | The specific behavior described in the issue (not a similar or adjacent symptom) is what the artifacts actually show | required |
| Outcome is stated honestly | The repro report's conclusion statement | The report states plainly whether the bug reproduced or not, and that statement matches what the artifacts actually show; an evidenced "could not reproduce" passes this check, a confident claim unsupported by the artifacts does not | required |
| Words respect repo conventions | The claim/repro comment text; the repo's contribution/AI policy | If the repo's policy requires disclosing AI use, the comment must contain an explicit disclosure statement (naming the tool and extent of assistance) — silence on AI use does not satisfy a mandatory-disclosure policy. The comment also does not promise a fix or a date, and breaks no rule in voice-guide.md | required |
| Package is proportionate to the issue | The repro report overall | The amount of investigation shown is proportionate to the issue's complexity (not padded, not thin) | preferred |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept (ready) if every `required` check passes. If any `required` check
fails, reject (hold). `preferred` checks never change the verdict — they
are informational only.

`unclear` counts as fail for `required` checks: if there isn't enough
evidence in the package to confirm a check passed, the package holds
rather than posts. `unclear` on a `preferred` check is ignored.