# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | Comment thread; repo-facts block (last commit date; whether this issue was opened by an OWNER/MEMBER/COLLABORATOR) | A maintainer/owner/collaborator commented on this issue OR opened it within the last 30 days, OR the default branch had a commit within the last 14 days | required |
| Repo in use | Repo-facts block (last commit date) | The default branch has had a commit within the last 30 days | required |
| Scope fits a newcomer | Issue body; comment thread | The issue describes one coherent task within a single subsystem — either (a) a documentation change (any number of files, each edit small and independent), or (b) a code change bounded to one file or one clearly-related area of the codebase (several similar, related fixes within the same subsystem still count as bounded) | required |
| Nobody else is on it | Repo-facts block (assignee field, linked PRs); comment thread | No assignee is set, AND there is no open linked PR addressing this issue, AND no comment anywhere in the thread claims active or completed work that hasn't been contradicted or superseded since | required |
| Not a claim graveyard | Comment thread (count of distinct claim/assignment attempts, especially bot-driven unassignment-for-inactivity notices) | Fewer than 3 prior claim-and-abandon cycles are visible in the thread | required |
| Repo accepts AI-assisted contributions | Repo-facts block (contribution policy field) | The contribution policy does not explicitly prohibit AI-generated code, documentation, or contributions | required |
| Has a beginner-friendly label | Repo-facts block (labels) | Issue carries a label such as `good-first-issue`, `beginner`, `starter`, or `help-wanted` | preferred |



## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->
Accept if every `required` check passes. If any `required` check fails, reject.
`preferred` checks never change the verdict — they only rank issues that were
already accepted, with more preferred-checks-passed ranked higher.

`unclear` counts as fail for `required` checks: if there isn't enough evidence
to confirm the issue is safe, we don't take the risk. `unclear` on a
`preferred` check is ignored (no bonus, no penalty).