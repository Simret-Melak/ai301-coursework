
---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Determine whether exactly one candidate pull request is ready to submit.

A PR package contains the proposed PR title and description, implementation diff, commits, test evidence, and the original plan, including documented deviations.

Compare the package against the issue's requirements, the original plan, the actual changes, the observed test results, and the repository's contribution standards.

Answer only whether the PR is ready to submit. Do not implement code, modify files, open a PR, or grade unrelated work.

Return exactly one binary verdict: `accept` or `reject`.

## Inputs and modes

Identify whether the invocation is in live mode or eval mode before gathering evidence.

### Live mode

Use live mode when reviewing the student's own proposed PR before opening it.

Read these inputs:

1. `plan.md`, including the diagnosis, scope, implementation approach, test plan, risks, and Deviations section.
2. The committed branch diff against the repository's main branch, obtained from the working repository with `git diff main...HEAD`.
3. The current branch name and commit information.
4. `pr_draft.md`, including the proposed PR title and complete description.
5. `test_evidence.md`, including reproduction steps, before-and-after results, and repository test commands.
6. The associated GitHub issue, its discussion, reproduction comments, and proposed solution.
7. The repository's `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`, including applicable AI-use and testing requirements.

Treat the committed diff as the authoritative record of what the PR changes. Do not count uncommitted working-tree edits as changes already included in the proposed PR.

For house-chain submissions, use the supplied house issue, reproduction pack, plan, branch, and test evidence instead of assuming the student authored the original issue or reproduction.

Compare the actual implementation against the plan and documented Deviations. Verify that the PR description accurately describes the changed files and recorded test outcomes.

Never claim that a test passed unless the supplied command output demonstrates that result.

### Eval mode

Use eval mode when the invocation supplies a frozen practice PR package or bundle identifier.

Treat the supplied package text as the complete evidence universe.

Read only the contents of that package, including its issue facts, plan, implementation, diff, PR description, test evidence, and repository policies or conventions.

Do not browse GitHub, fetch external information, inspect the local working repository, or supplement missing package information with assumptions.

Do not read `scope.md` or `voice-guide.md` in eval mode.

Execute every check in `rubric.md` and apply its complete verdict rule. Do not skip checks simply because a package appears clearly acceptable or unacceptable.

## The scope seam (live mode only)

Before grading a live submission, read `scope.md`.

Identify the repository named in its `Repo:` field and the stated environment and contribution requirements.

If the `Repo:` field contains an unresolved placeholder, stop without grading. Explain that the student must replace the placeholder with the correct Path Review repository.

For this course section, the scoped repository is:

`codepath/pathreview-ai301-fa26-s1`

Verify that the issue and intended PR target belong to this repository.

If the proposed PR targets a different repository, refuse to grade it. Do not silently substitute another repository or guess the intended target.

Use the remaining scope rules to determine which changes and evidence belong to the permitted environment.

Ignore `scope.md` entirely in eval mode.

## The voice seam (live mode only)

Read `voice-guide.md` before evaluating the outgoing PR title and description.

Check whether the student's proposed communication follows the guide's rules for respectful, evidence-based, professional upstream contributions.

Identify specific violations, quoting the relevant rule and offending text where possible.

Report voice-guide findings in the readable summary before the JSON output.

A voice-guide violation does not independently change the final verdict unless a check in `rubric.md` explicitly incorporates that requirement.

In eval mode, ignore `voice-guide.md`. Grade communication quality only through the universal checks defined in the rubric.

## Component reads

Use the components in the installed skill directory as follows:

1. Read `rubric.md` to identify every required and preferred check, its evidence sources, pass condition, and weight.
2. Read `references/evidence-guide.md` to locate the evidence needed for each check.
3. Read `procedure.md` and execute its steps in their stated order.
4. Gather evidence from the permitted sources for the selected mode.
5. Grade every rubric check using the stated pass condition.
6. Apply the verdict rule defined in `rubric.md`.

Do not invent additional grading criteria or override an explicit rubric rule with personal judgment.

If a procedure step is missing or unclear, report the gap rather than inventing an undocumented procedure.

If `rubric.md` or `procedure.md` contains no substantive student-authored content beyond template comments or placeholders, refuse to grade and explain which component must be completed.

Do not generate a fabricated acceptance or rejection when required grading components are empty.

## Verdict and output

The final verdict must be binary:

- `accept`: the PR satisfies the rubric's requirements and is ready to submit.
- `reject`: the PR does not satisfy the rubric's requirements and should be held for revision.

Use the exact verdict rule in `rubric.md`.

For each rubric check, report:

- Its exact name.
- A grade of `pass`, `fail`, or `unclear`.
- One concise line identifying the specific evidence supporting the grade.

Before the machine-readable result, provide a short human-readable summary of the checks and any important findings.

End the response with the following fenced JSON block. Replace the placeholders with the actual item identifier, check results, evidence, and verdict.

Keep this JSON schema unchanged, valid, and last. Do not add any text after the closing code fence.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

Follow these standing rules on every evaluation:

1. **Evidence first.** Support each grade with an identifiable fact, command result, file change, or quotation from an allowed source. Never use "looks good" or general impressions as evidence.

2. **Grade substance rather than presentation.** A short but complete PR may be acceptable. A polished description does not compensate for missing tests, implementation drift, or incorrect claims.

3. **Compare plan and implementation.** Verify that changed files and behavior correspond to the original plan or explicitly documented Deviations. Detect unexplained additions, omitted changes, and unrelated modifications.

4. **Verify testing claims.** Compare the described testing against actual commands and outputs. Distinguish passing, failing, skipped, and expected-failure tests. Never interpret an `XFAIL` as proof that the intended application behavior has been fixed.

5. **Assess reviewability.** Determine whether another contributor can understand the purpose, changed behavior, test evidence, and remaining limitations of the proposed PR.

6. **Apply repository standards.** Check the applicable PR template, issue requirements, contribution rules, and disclosure requirements. In live mode, include the course's required AI-use disclosure in the PR description.

7. **Let the rubric decide.** Grade each check strictly according to its written pass condition. Do not change a grade because the final verdict feels surprising.

8. **Let the procedure decide how.** Follow `procedure.md` as written. Report missing procedural guidance rather than silently replacing it.

9. **Handle uncertainty explicitly.** Use `unclear` when the available evidence cannot establish whether a check passes or fails. If the rubric's verdict rule does not specify otherwise, treat `unclear` as failing for verdict purposes.

10. **Never invent results.** Do not fabricate tests, CI results, issue discussions, repository policies, screenshots, or implementation evidence.

11. **Grade one package only.** Do not combine evidence or verdicts from separate PR packages.

12. **Preserve the required output.** Emit one complete, valid JSON result as the final fenced block, with nothing after it.
