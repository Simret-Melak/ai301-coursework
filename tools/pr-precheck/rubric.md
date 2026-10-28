
# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Implementation matches the plan | The changed files and behavior in the PR diff, read against the plan's scope, approach, and Deviations section | Every substantive change is described in the plan or its documented Deviations. A smaller or different implementation is acceptable when the difference is explicitly disclosed and the PR description accurately states what was delivered. Undisclosed changes or omissions that contradict the plan fail. | required |
| PR claims match the implementation | The PR title, summary, and changes description, compared with the actual diff and the plan | Every material claim about implemented behavior is supported by the diff. The description distinguishes completed work from planned or omitted work and does not claim that an unimplemented fix is complete. An honestly disclosed shortfall can pass. | required |
| Testing provides observable evidence | The test evidence's commands, outputs, and before/after observations, compared with the plan's test plan and the PR's testing claims | The evidence demonstrates what was actually checked and the observed result. Relevant behavior changes or remaining failures are identifiable. A failing or incomplete test can pass when accurately reported and its implications are disclosed; unsupported claims that the fix works fail. | required |
| Repository checks are accounted for | The test evidence and PR testing section, read against the repository's required test, lint, typecheck, and integration checks | Each applicable repository check has an identifiable command and recorded outcome, or a specific disclosed reason it could not be run. Expected absence of integration tests is not treated as a successful integration test. Missing checks silently presented as completed fail. | required |
| Diff is focused and reviewable | The diff's changed files and hunks, compared with the plan's scope and the issue requirements | The diff contains only changes reasonably necessary for the issue or documented deviations. It has no unrelated cleanup, debug artifacts, accidental generated files, or commented-out experimental code that obscures the contribution. A concise or complex diff can pass if its changes are relevant and understandable. | required |
| PR description is reviewable | The PR title and description, read against the diff, test evidence, issue, and plan | A maintainer can identify the purpose of the PR, what changed, how it was tested, and any limitations without relying on unsupported assertions. Brevity or formatting alone does not fail this check. | required |
| Repository standards are satisfied | The repository-facts block, PR template, contribution and AI policies, read against the PR title, description, and test disclosures | The PR satisfies applicable repository-specific requirements, including required template information and AI-use disclosure where required. Explicit disclosure of a known testing limitation is acceptable when the stated policy permits it. Omitting a mandatory disclosure or materially required information fails. | required |
| Issue and branch are consistent | The issue reference and repository facts, compared with the PR's branch and described purpose | The PR identifies the intended issue, and its stated purpose is consistent with that issue. A branch naming requirement is enforced only when established by the repository or course rules supplied in the evidence. | preferred |

## Verdict rule

Grade every check as `pass`, `fail`, or `unclear`, using the evidence and pass condition in its row.

Return `accept` only when every `required` check passes. Return `reject` when at least one `required` check fails or is unclear.

An `unclear` grade counts as a failure for required checks because the available evidence does not establish that the PR is ready to submit.

`preferred` checks provide useful feedback but never change the final verdict, whether they pass, fail, or are unclear.

Evaluate the substance of the PR rather than the length, style, or polish of its description.

An honestly disclosed shortfall is not an automatic rejection. Judge whether the PR accurately represents what was delivered, identifies remaining limitations, and provides the evidence required by the applicable checks.

Do not invent test results or repository requirements. Use only the sources permitted by the selected mode.

The final verdict is binary: `accept` (ready to submit) or `reject` (hold).
