# Contribution: Add Testing for Pub/Sub Message Attributes (Candidate)

Path: `beat-2-contribution/contribution-story.md`

**Contribution Number:** [1]  
**Student:** [Your CodePath student name]  
**GitHub Username:** Simret-Melak  
**Issue:** https://github.com/apache/beam/issues/18832  
**Pull Request:** Not opened yet

*Apache Beam #18832 is my current leading candidate based on Unit 5 grading. I have not yet claimed or committed to this issue. I will confirm my final selection in Unit 6.*

---

## Toolkit

I am documenting the AI-assisted tools I build and use throughout my first real open-source contribution. Each weekly entry records what I built, what I learned, what did not work as expected, and how I responded.

**Unit 5: Built issue-scout and improved GitHub issue discovery**

I upgraded my Unit 1 `issue-select` skill into `issue-scout`, preserving my original rubric and evidence guide while creating a search strategy focused on Python, Java, backend development, testing, and AI integration. My first scan retrieved 300 GitHub issues and graded five, accepting four and rejecting one. The scan revealed that my ranking favored very recently updated issues, sometimes from the same small repository, so I changed the strategy to allow only one candidate per repository and documented why I did not impose a minimum star requirement. I then used the scout to grade three candidates from the CodePath Issue Selection site; Apache Beam #18832 was accepted, while ArduPilot #14438 and Xplore-workshop #21 were rejected.

**Unit 6: [Voice-guard and repository memory — pending]**

To be completed during Unit 6 after choosing and claiming my final issue.

**Unit 7: [Ship-gate and implementation verification — pending]**

To be completed during Unit 7 after implementing and testing the contribution.

**Unit 8: [PR-monitor and maintainer communication — pending]**

To be completed during Unit 8 after opening and monitoring my real open-source pull request.

---

## Why I Chose This Issue

During Unit 5, I wanted to find an open-source issue that matched my programming experience while giving me an opportunity to strengthen my testing and Python or Java development skills. I am most comfortable with Java and have experience with Python and JavaScript, and I prefer backend and testing tasks over frontend development. I created an `issue-scout` search strategy that used GitHub CLI to search for open beginner-friendly issues, including Python bugs, tests, and Java issues.

My first automated scan collected 300 issues and evaluated the top five. Four were accepted. However, I noticed that the ranking strongly favored very recent issues and sometimes selected multiple issues from small repositories. To improve the variety of results, I updated the ranking rules to limit the final candidate list to one issue per repository. I documented this change in `scan-notes.md` and did not claim that it had been validated by a second scan.

I then selected three issues from the CodePath Issue Selection site and graded them using my scout:

- [Apache Beam #18832 — Add testing for Pub/Sub attributes](https://github.com/apache/beam/issues/18832): ACCEPT
- [ArduPilot #14438 — Modify autotest to notify Discord](https://github.com/ArduPilot/ardupilot/issues/14438): REJECT
- [Xplore-workshop #21 — CLI login/signup system](https://github.com/ProjectX-VJTI/Xplore-workshop/issues/21): REJECT

Apache Beam #18832 became my leading candidate because the scout identified a bounded Java SDK integration-testing task related to Pub/Sub message attributes. The issue matches my Java and testing interests and offers an opportunity to learn about integration tests in a large, established project. My scout reported an active repository, no current assignee, and no linked pull request at the time of grading.

I also learned that a beginner-friendly label does not necessarily mean an issue is suitable. The ArduPilot issue involved uncertain CI and server infrastructure work, while Xplore-workshop had evidence of limited maintainer activity and an existing contributor claim. My scout helped identify these concerns, although its earlier ranking problems showed that search results still require careful investigation.

**Claim comment:** Claim pending — November 11, 2026. I will add the actual GitHub claim-comment URL in Unit 6 once I make my final selection.

**Toolkit**

- **Tool:** `issue-scout`, using my GitHub search strategy, Unit 1 rubric, scope profile, and evidence guide.
- **What it produced:** An automated scan of 300 issues, five initial grading verdicts, and three direct-URL grading verdicts for CodePath candidates. Apache Beam #18832 was accepted.
- **Difficulties:** My first scan overrepresented recently updated issues from small repositories. Two initial candidates also came from the same repository, reducing diversity.
- **What changed:** I revised the ranking strategy to allow at most one issue per repository, documented the limitations in `scan-notes.md`, and kept repository popularity as a consideration rather than an automatic rejection rule. I did not rerun the scan after this change.

---

## Understanding the Issue

**Problem Description**

Based on the Apache Beam issue description, additional integration-test coverage is needed for reading and writing Pub/Sub message attributes through the Java SDK. My initial understanding is that the task concerns missing test coverage rather than a confirmed production failure.

I will investigate the relevant code and existing tests during Unit 6.

**Expected Behavior**

An integration test should exercise the supported handling of Pub/Sub message attributes when messages are written and read. The test should verify the intended behavior using assertions rather than merely checking that the process completes.

The precise acceptance criteria still need to be confirmed from the existing code, tests, and maintainer guidance.

**Current Behavior**

The issue identifies missing integration-test coverage for Pub/Sub attributes. I have not yet reproduced the gap locally or confirmed whether related test coverage has been added since the issue was opened.

I will verify the current repository state before beginning implementation.

**Affected Components**

Potentially affected areas include:

- Apache Beam Java SDK.
- Google Cloud Pub/Sub integration.
- Existing Pub/Sub integration tests and test utilities.

Specific files, classes, and methods will be recorded after inspecting the repository.

**Toolkit**

- **Tool:** `issue-scout` for issue investigation and suitability grading.
- **What it produced:** An ACCEPT verdict for Apache Beam #18832 based on reported repository activity, scope, issue discussion, and contribution-policy evidence.
- **Difficulties:** The grading process assessed issue suitability but did not reproduce the missing test coverage or identify exact implementation files.
- **What changed:** I will use the Unit 6 reproduction workflow and code inspection to confirm the behavior before proposing a solution.

---

## Reproduction Process

**Environment Setup**

Pending Unit 6.

My development environment uses macOS. I will record the exact Java version, build-tool version, Apache Beam commit, dependencies, and setup commands after preparing the project locally.

I have not yet cloned and configured Apache Beam specifically for this issue.

**Steps to Reproduce**

1. Clone and configure the selected repository — pending.
2. Locate the existing Pub/Sub integration tests and determine the missing attribute coverage — pending.
3. Run the relevant baseline tests and record their observable results — pending.

**Reproduction Evidence**

- **Commit showing reproduction:** Pending.
- **Screenshots/logs:** Pending.
- **My findings:** Issue Scout identified the missing coverage described by the issue, but no local reproduction has been completed.

**Toolkit**

- **Tool:** Unit 6 reproduction workflow — pending.
- **What it produced:** Pending.
- **Difficulties:** Pending.
- **What changed:** Pending.

---

## Solution Approach

**Analysis**

Pending code inspection and reproduction.

The issue suggests missing integration-test coverage for Pub/Sub attributes. I have not yet established the exact code path or confirmed whether the expected test behavior is already covered elsewhere.

**Proposed Solution**

My tentative approach is to extend the relevant Java SDK integration tests to exercise Pub/Sub message attributes, using the repository's existing test patterns.

The final approach will be based on the repository's implementation and maintainer requirements. I do not plan to change unrelated production functionality merely to add test coverage.

**Implementation Plan**

1. Inspect the Pub/Sub test infrastructure and identify the appropriate existing test suite.
2. Determine the attribute-writing and attribute-reading behavior that requires coverage.
3. Add or update the integration test and relevant assertions.
4. Run the targeted test and required repository checks.
5. Document any deviations between the original plan and the actual implementation.

This is a preliminary outline, not a completed or validated implementation plan.

**Toolkit**

- **Tool:** Planning skill and repository investigation — pending.
- **What it produced:** Pending.
- **Difficulties:** Pending.
- **What changed:** Pending.

---

## Testing Strategy

The intended testing strategy is to establish a baseline, introduce the missing integration-test coverage, and run the relevant tests again.

The final evidence should record:

1. The exact baseline command and its output.
2. The new or updated test and the attribute behavior it asserts.
3. The targeted integration-test command and result.
4. Any applicable build, formatting, lint, or other repository checks.
5. Any failures, unavailable external services, or environmental limitations.

No Apache Beam tests have been run locally for this contribution yet.

**Toolkit**

- **Tool:** Test and verification workflow — pending.
- **What it produced:** Pending.
- **Difficulties:** Pending.
- **What changed:** Pending.

---

## Implementation Notes

**November 5–6, 2026 — Preparing Issue Scout**

I installed GitHub CLI and authenticated it with my GitHub account. I backed up my Unit 1 `issue-select` skill before installing the Unit 5 starter files and renaming the installed skill to `issue-scout`. I preserved the existing rubric and evidence guide and wrote a search strategy based on my Java, Python, backend, and AI interests.

**November 6, 2026 — Running My First Scan**

I ran `issue-scout: run a scan`. The scout retrieved 300 issues from three GitHub searches and graded the top five, returning four ACCEPT verdicts and one REJECT verdict.

The scan revealed that my ranking strongly favored recently updated, low-comment issues, including multiple candidates from the same small repository.

**November 6, 2026 — Improving the Search Strategy**

I updated the ranking strategy to allow at most one issue per repository in the final candidate list. I retained the 90-day activity filter and beginner-friendly labels. I decided not to enforce a minimum number of GitHub stars because popularity does not always indicate project quality or maintainer support.

I documented the update in `scan-notes.md`. I did not perform a second paid scan, so the improvement remains unverified by a new scan.

**November 11, 2026 — Grading CodePath Candidates**

I used the CodePath Issue Selection site to identify three possible issues and submitted their GitHub URLs to `issue-scout`.

The scout accepted Apache Beam #18832, describing it as a focused Java SDK testing task. It rejected ArduPilot #14438 because the implementation scope appeared to extend into CI/server infrastructure. It rejected Xplore-workshop #21 because of maintainer inactivity and evidence of an existing contributor's claim.

I identified Apache Beam #18832 as my leading candidate for Unit 6 but have not yet claimed it or started implementation.

**Toolkit**

- **Tool:** `issue-scout`, GitHub CLI, search strategy, and issue-selection rubric.
- **What it produced:** A saved scan, grading results for eight issues across two runs, and notes documenting the ranking limitations.
- **Difficulties:** The first scan favored recently created issues and lacked sufficient repository diversity. The initial direct grading of three CodePath candidates accepted only one.
- **What changed:** I updated the ranking strategy, documented the trade-offs, and kept Apache Beam #18832 as a candidate requiring further verification before claiming.

---

## Pull Request

**PR Link:** Not opened yet.

**PR Description:** Pending implementation. The eventual PR will explain the issue, the implemented changes, the tests performed, any known limitations, and applicable AI-assistance disclosures.

**Maintainer Feedback**

- November 11, 2026: No feedback requested or received for this contribution yet.
- Pending: Record maintainer feedback and responses when they occur.

**Status:** Not opened — issue-selection stage.

**Toolkit**

- **Tool:** PR preparation, precheck, and monitoring tools — pending.
- **What it produced:** Pending.
- **Difficulties:** Pending.
- **What changed:** Pending.

---

## Learnings and Reflections

**Technical Skills Gained**

During Unit 5, I learned how to use GitHub CLI to search issues by language, label, and status. I practiced designing an automated workflow that separates inexpensive searching and ranking from more expensive rubric-based evaluation.

I also learned how to evaluate repository activity, issue ownership, maintainer responsiveness, contribution policies, and task scope before choosing an open-source issue.

**Challenges Overcome**

One challenge was installing GitHub CLI on my Mac. Homebrew installation failed because the download process could not locate its expected SSL certificate file. I used the official GitHub CLI macOS installer instead and successfully authenticated my GitHub account.

Another challenge was that my initial scout ranking favored newly updated issues from small repositories, including repeated results from the same project. I addressed this by adding a one-issue-per-repository ranking rule and documenting why I made that change.

**What I'd Do Differently Next Time**

I would consider repository diversity and maintainer engagement earlier when designing the search strategy. I would also avoid assuming that a `good first issue` label guarantees an issue is manageable or available.

Before claiming an issue, I will verify that it is still relevant, inspect its discussion and linked pull requests, and evaluate the likely environment setup requirements.

---

## Resources Used

- [GitHub CLI documentation](https://cli.github.com/manual/)
- [GitHub issue-search documentation](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests)
- [CodePath AI301 Issue Selection site](https://open-source-issue-tracker.onrender.com/)
- [CodePath Unit 5 starter repository](https://github.com/codepath/ai301-unit5-starter)
- [Apache Beam Issue #18832](https://github.com/apache/beam/issues/18832)
- [ArduPilot Issue #14438](https://github.com/ArduPilot/ardupilot/issues/14438)
- [Xplore-workshop Issue #21](https://github.com/ProjectX-VJTI/Xplore-workshop/issues/21)
