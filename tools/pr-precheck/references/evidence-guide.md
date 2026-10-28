
# Evidence guide: where evidence lives in a PR package

This guide identifies the evidence sources used to grade a candidate pull request. It applies the same rubric to both live PR drafts and frozen evaluation packages.

In live mode, use the student's working repository, issue thread, plan, PR draft, and recorded test evidence.

In eval mode, use only the text contained in the supplied package. Do not fetch GitHub content, inspect the local repository, or invent missing facts.

For every check, identify the actual evidence before assigning a grade. Compare artifacts against one another rather than relying on the candidate's claims alone.

## Plan fidelity (harness category: silent-drift)

### Where it lives

**Eval mode:**

- Read the package's plan-context block for the planned scope, affected files or functions, intended behavior, exclusions, and documented deviations.
- Read the candidate PR's changed-file list, commits, and unified diff to determine what was actually implemented.
- Read the candidate PR title and description for claims about what was completed, changed, omitted, or intentionally deferred.
- Use the issue description and thread highlights to understand the original problem and any maintainer-approved changes in direction.

**Live mode:**

- Read `plan.md`, including its diagnosis, Scope, Files, Approach, Test plan, and `## Deviations` sections.
- Run `git diff main...HEAD` from the PathReview working repository to inspect the committed branch changes.
- Use `git diff main...HEAD --stat` to identify all changed files.
- Read `pr_draft.md` to compare the proposed title, Summary, Changes, and Notes for Reviewers against the actual diff.
- Review the associated GitHub issue and relevant discussion for the intended contribution.

### What good looks like

Every substantive change in the diff corresponds to the original plan or an explicitly documented deviation.

The PR description accurately distinguishes implemented work from deferred or incomplete work.

A smaller or modified implementation can be acceptable if the shortfall is disclosed, the plan's Deviations explain the change, and the PR does not claim to deliver behavior that is absent.

### Failure signals

- Changed files or functions fall outside the plan without an explanation.
- A planned behavior is omitted without disclosure.
- The PR claims that a fix was implemented when the diff contains only supporting tests.
- The PR description claims full plan compliance while the actual implementation differs materially.
- Deviations are concealed or contradict the evidence.

Do not reject a PR solely because its implementation differs from the original plan when the difference is documented and accurately represented.

## Test evidence (harness category: not-tested)

### Where it lives

**Eval mode:**

- Read the plan-context block's test plan and the original reproduction steps.
- Read the candidate PR's test-evidence section for executed commands, expected results, observed results, and recorded output.
- Read the PR description's testing claims and checkboxes.
- Read repository facts or template instructions identifying required checks.

**Live mode:**

- Read the Test plan in `plan.md`.
- Read `test_evidence.md` for recorded reproduction steps, command outputs, and test outcomes.
- Compare those results with the original reproduction from the issue thread.
- Read the Testing section of `pr_draft.md`.
- Check the repository's `.github/PULL_REQUEST_TEMPLATE.md` for required verification commands.

For PathReview, the relevant checks include:

- `make test-unit`
- `make test-integration`
- `make lint`
- `make typecheck`

Record the outcome of each check without changing or inventing its result.

### What good looks like

The evidence identifies what was executed, what result was expected, and what actually happened.

Before-and-after observations can be connected to the issue and the plan's test expectations.

The PR accurately describes successful, failing, skipped, unavailable, and expected-failure tests.

A command that fails can still provide useful evidence when its failure and implications are disclosed honestly.

A test marked `XFAIL` demonstrates an expected failure, not a successful behavioral fix. An unexpected pass (`XPASS`) must also be identified accurately.

A repository check that reports no tests collected must not be described as a successful test run.

### Failure signals

- The PR claims tests passed without any supporting execution evidence.
- Commands are listed without observable outcomes.
- A claimed behavioral fix is not supported by the recorded before-and-after evidence.
- Required repository checks are silently omitted.
- Failing tests are described as passing.
- Expected failures are misrepresented as proof of a working fix.
- The PR's Testing section contradicts the supplied output.

A disclosed testing limitation is not automatically grounds for rejection. Apply the rubric's pass conditions to determine whether the evidence is sufficient and accurately represented.

## Diff quality (harness category: unreviewable)

### Where it lives

**Eval mode:**

- Read the candidate PR's unified diff.
- Inspect the changed-file list and commit summaries.
- Compare each changed file with the issue requirements, plan scope, and documented deviations.
- Use the PR description to understand the stated purpose of each material change.

**Live mode:**

- Run `git diff main...HEAD` to inspect the committed changes.
- Run `git diff main...HEAD --stat` to identify the complete changed-file list.
- Inspect the relevant changed hunks, additions, and deletions.
- Compare the diff with `plan.md`, including `## Deviations`.
- Read `pr_draft.md` to verify that its Changes section represents the diff accurately.

### What good looks like

The diff is limited to changes necessary for the issue or changes explicitly explained in documented deviations.

A reviewer can identify the implementation and understand why the modified files are relevant.

Necessary supporting tests, fixtures, configuration changes, or documentation may be appropriate when connected to the issue.

A large diff is not automatically unreviewable, and a small diff is not automatically acceptable. Judge the relevance and clarity of the actual changes.

### Failure signals

- Unrelated refactoring or formatting changes obscure the intended fix.
- Debug statements or temporary logging remain without justification.
- Dead code, commented-out experiments, or abandoned implementations remain in the diff.
- Generated files, temporary outputs, or unrelated artifacts are accidentally committed.
- Significant changes have no relationship to the plan, documented deviations, or issue.
- The intended implementation cannot be identified among unrelated edits.

Do not reject useful supporting changes merely because they involve additional files. Determine whether they are necessary for the contribution.

## Standards and comms (harness category: standards-wall)

### Where it lives

**Eval mode:**

- Read the package's repository-facts block for the PR template, contribution requirements, and stated policies.
- Read the issue thread highlights for maintainer instructions and existing discussion.
- Read the candidate PR title and description, including testing, issue references, screenshots, reviewer notes, and disclosures.
- Use only policies explicitly included in the package.

Do not invent repository standards or import rules from a different repository.

**Live mode:**

- Read `.github/PULL_REQUEST_TEMPLATE.md` for the required PR sections and testing checklist.
- Read `docs/CONTRIBUTING.md` for relevant contribution and testing conventions.
- Read applicable repository AI-use policies when present.
- Read the associated GitHub issue and maintainer comments.
- Read `pr_draft.md`, including the title, Summary, Issue, Changes, Testing, Screenshots / Demo, and Notes for Reviewers.
- Read `voice-guide.md` for the student's communication rules.

The CodePath Unit 4 assignment also requires a description of how AI was used in the contribution. This disclosure belongs in Notes for Reviewers.

### What good looks like

The PR follows the applicable repository requirements and supplies the information a maintainer explicitly requested.

The issue reference identifies the intended contribution.

Required template sections contain relevant information rather than empty placeholders or unsupported boilerplate.

Testing claims accurately describe the recorded results.

Mandatory AI-use disclosures identify the assistance used in a way that satisfies the stated policy.

Explicit maintainer guidance is acknowledged or addressed.

If screenshots are not relevant, an explanation such as "N/A — backend test-only change" can be sufficient when the template permits it.

### Failure signals

- A mandatory PR template section is missing or left as an unanswered placeholder.
- Required AI-use disclosure is absent.
- The PR contradicts explicit maintainer instructions without an explanation.
- Required testing information is silently omitted.
- The PR ignores an applicable contribution policy.
- The description contains claims that cannot be reconciled with its evidence.

Whether implementation claims match the actual diff is primarily graded under Plan fidelity. Do not duplicate that judgment merely because the claim appears in the description.

### General evidence rules

1. Use only evidence permitted by the selected mode.
2. Preserve the distinction between observed results and contributor claims.
3. Quote or identify the specific fact supporting each check.
4. Do not infer a successful test from the absence of reported errors.
5. Do not interpret disclosed limitations as automatic failures.
6. Treat genuinely missing evidence as `unclear` unless the rubric's pass condition establishes a definite failure.
7. Apply the verdict rule from `rubric.md` consistently.
8. Never invent an issue discussion, repository policy, test outcome, or implementation detail.
