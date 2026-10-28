
# Procedure: how this tool grades a PR package

## Read order

1. Identify the invocation mode before reading package evidence. Use live mode for the student's own draft PR, and eval mode for a frozen practice package. Grade exactly one package per invocation.

2. Read `rubric.md` and `references/evidence-guide.md`. Identify every check, its evidence sources, pass condition, weight, and the verdict rule. Do not start grading until the complete list of checks is known.

3. In live mode, read `scope.md` before accessing the student's submission. Confirm that its `Repo:` field contains a real repository rather than a placeholder. Confirm the proposed issue and PR target belong to that repository. Refuse to grade an unconfigured or out-of-scope submission. Also read `voice-guide.md` for the outgoing title and description. In eval mode, ignore both files.

4. Read the issue and its reproduction evidence first. In live mode, obtain the real issue thread, relevant comments, repository contribution rules, and PR template. In eval mode, read only the issue facts, thread highlights, and repository policies included in the bundle. Record the issue's requested outcome and any explicit contribution requirements.

5. Read `plan.md` before examining the implementation. Record the proposed change, affected files and functions, exclusions, test plan, and `## Deviations` entries. In eval mode, use the corresponding plan and deviations from the frozen package.

6. Read the implementation next. In live mode, inspect the committed changes using `git diff main...HEAD` and record the current branch name. In eval mode, read the supplied changed-file list, commits, and diff. Record all changed paths and substantive behavior changes. Do not treat uncommitted edits as part of the submitted PR.

7. Read the test evidence after understanding the planned and actual change. In live mode, inspect `test_evidence.md`; in eval mode, inspect the package's testing evidence. Record actual commands, outputs, observed behavior, and any limitations.

8. Read the draft PR title and description last. In live mode, use `pr_draft.md`; in eval mode, use the title and description provided by the package. Record claims about implementation, testing, issue resolution, screenshots, deviations, and disclosures.

9. Keep the reading order consistent. Reading the plan before the diff prevents the implementation from redefining the planned scope. Reading the description after the evidence allows its claims to be checked independently.

## Evidence gathering

1. **Plan fidelity:** Create a side-by-side comparison of the plan's stated changes and the diff's actual changes. Record each planned file or behavior, whether it appears in the diff, and any extra changed files or behavior. Check the plan's Deviations section for explicit explanations of differences.

2. **Implementation claims:** Extract every material claim from the PR title, Summary, Changes, and Notes for Reviewers. Match each claim to a corresponding diff hunk or documented limitation. Record any claimed fix that the diff does not establish, any implemented change omitted from the description, and any discrepancy between the plan and the PR.

3. **Observable test evidence:** Compare the plan's test plan against the test evidence. Record the reproduction commands or steps, their before-and-after results, and the observed outcome. Distinguish passing tests, failing tests, expected failures (`XFAIL`), unexpected passes (`XPASS`), skipped checks, and tests that were not run. Do not interpret an XFAIL as proof that the underlying application behavior has been fixed.

4. **Repository checks:** Identify required testing commands from the repository's PR template or stated policy. In live mode, specifically inspect evidence for `make test-unit`, `make test-integration`, `make lint`, and `make typecheck` when applicable. In eval mode, use only the checks and standards included in the package. Record each command's reported outcome or its explicitly disclosed reason for not being run.

5. **Diff quality:** Inspect each changed file and relevant diff hunk. Record unrelated modifications, debugging statements, generated artifacts, accidental files, commented-out experiments, or other material that obscures the intended contribution. Do not reject a change merely because its diff is large, small, or formatted differently.

6. **Reviewability:** Compare the PR description with the issue requirements, plan, changed files, and test evidence. Determine whether a maintainer can identify what the PR actually delivers, why the change was made, what was tested, and what remains unresolved.

7. **Repository standards and communication:** Read the repository's PR template, contribution rules, and AI-use policy when present. Compare their explicit requirements with the submitted description. In live mode, also check the course-required AI-use disclosure and apply the voice-guide rules, reporting any violations separately. In eval mode, never assume repository policies that the package does not provide.

8. **Issue and branch consistency:** Record the issue identifier, repository, branch name, and PR target where available. Determine whether the PR concerns the stated issue and whether an applicable branch naming rule is satisfied.

9. For every collected fact, retain its source: a file path, diff hunk, command output, plan statement, repository rule, or short quotation from the package. Do not replace missing evidence with assumptions.

## Check execution

1. Execute all eight rubric checks in their written order. Do not stop after finding one failed required check.

2. For each check, identify the evidence sources named in its rubric row. Use the evidence already gathered, consulting `references/evidence-guide.md` when the source location is unclear.

3. Grade `Implementation matches the plan` by comparing actual substantive changes with the plan and its documented Deviations. Pass if changes and omissions are accounted for and the PR accurately states what was delivered. Fail for undisclosed drift.

4. Grade `PR claims match the implementation` by matching material claims in the title and description to the actual diff. Pass when claims are supported and limitations are accurately disclosed. Fail when the PR asserts behavior the implementation does not provide.

5. Grade `Testing provides observable evidence` by comparing recorded commands and observations with the plan's test expectations and the PR's testing claims. Pass when the evidence demonstrates what happened and shortcomings are honestly described. Fail for fabricated, contradictory, or unsupported success claims.

6. Grade `Repository checks are accounted for` by examining each applicable required check and its recorded result or disclosed reason for omission. Do not mark an unavailable or unrun test as passed. Fail if a required check is silently omitted or misrepresented.

7. Grade `Diff is focused and reviewable` by inspecting the changed files and hunks against the issue and plan. Fail for unrelated changes or debris that materially obscures the contribution.

8. Grade `PR description is reviewable` by checking whether the stated purpose, implemented changes, testing, and limitations can be understood from the supplied evidence. Do not judge by length, formatting, or writing polish alone.

9. Grade `Repository standards are satisfied` against the actual requirements contained in the permitted evidence. Fail for an omitted mandatory template field, disclosure, or other material requirement. Do not invent policies that are absent from the evidence.

10. Grade `Issue and branch are consistent` using the supplied issue, target, branch, and applicable naming requirements. This is a preferred check and does not independently change the final verdict.

11. Assign `pass` only when the available evidence satisfies the stated pass condition. Assign `fail` when the evidence contradicts the pass condition. Assign `unclear` when a necessary fact is missing and neither a pass nor a definite failure can be established.

12. For each check, write one concise evidence line identifying the deciding fact, quotation, file change, or test output. Do not write generic statements such as "looks correct" or "seems incomplete."

13. An honestly disclosed limitation is not an automatic rejection. Apply the specific pass condition to determine whether the disclosure is adequate and whether the PR accurately represents its outcome. Do not excuse unrelated changes or mandatory repository requirements merely because they are disclosed.

14. If a required evidence source or procedural step is unavailable, report that limitation explicitly. Do not invent facts or silently substitute a different grading method.

## Verdict assembly

1. Collect all check results in the exact order they appear in `rubric.md`.

2. Apply the rubric's verdict rule: return `accept` only if every required check is graded `pass`. Return `reject` if any required check is graded `fail` or `unclear`.

3. Preferred checks provide feedback but do not change the verdict, regardless of whether they are graded `pass`, `fail`, or `unclear`.

4. When multiple required checks fail, identify the first failing required check in rubric order as the primary reason for rejection. Include the other failed or unclear checks in the summary. Use the primary check's deciding fact or quotation when explaining the overall verdict.

5. When the verdict is `accept`, identify the strongest concrete evidence supporting readiness and mention any disclosed limitations without changing the verdict.

6. Produce a short, readable summary listing each check, its grade, and the evidence that determined it. In live mode, also report voice-guide violations separately when applicable.

7. Set the JSON `item` value to the PR URL or issue-associated draft identifier in live mode, or the exact bundle ID in eval mode.

8. End the response with one fenced `json` block using the unchanged schema in `SKILL.md` and `CONTRACT.md`. Include every rubric check with its exact name, grade, and one-line evidence.

9. Set `verdict` to exactly `accept` or `reject`. Do not add other verdict values, scores, or fields to the JSON.

10. Ensure the JSON is valid and the final fenced block is the last content in the response. Nothing may appear after it.
