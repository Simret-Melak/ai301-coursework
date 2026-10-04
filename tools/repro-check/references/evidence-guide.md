# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: in an eval bundle, the repro report's environment
section (OS, language/runtime version, dependency versions, install
commands run), read against the issue's repo-facts block (what
versions/platforms the issue targets or was filed against). In live
mode, the student's draft repro comment, read against the repo's own
setup docs (README, CONTRIBUTING, or a docs/ setup guide) and the
issue thread itself for any stated target environment.

What good looks like: every version or tool named in the environment
record is either an exact match to what the issue targets, or any
difference is explicitly called out and explained (e.g. "issue was
filed against v2.1, I reproduced on v2.3, behavior is identical"). A
report that omits a version number the issue explicitly depends on is
insufficient, even if everything else is well written.

## Steps

Where it lives: the repro report's step-by-step section, in an eval
bundle or a live draft. Read start to finish, starting state to
triggering action.

What good looks like: a stranger with a clean checkout of the repo
could follow the steps in order and arrive at the same triggering
action with no unstated assumptions (no skipped installs, no "you'll
also need to configure X" left out, no step that only makes sense if
you already know the codebase). A step is followable if it names an
exact command, file, or UI action — not a vague description of intent
("set up the test data" is not followable; "run `make seed-test-db`"
is).

## Behavior shown

Where it lives: the artifacts section of the repro report (pasted
output, error messages, logs, screenshots), read directly against the
issue's own description of the bug (its title, body, and any error
text quoted in the original issue).

What good looks like: the artifact shows the SAME symptom the issue
names — same error type, same incorrect output, same crash — not a
merely similar-looking problem in a nearby part of the code. If the
issue describes a specific error message or stack trace, the artifact
should show that same error (or a clear, explained equivalent), not a
different error that happens to occur in the same function.

## Honesty

Where it lives: the repro report's concluding statement, read against
everything above it (environment, steps, artifacts).

What good looks like: the stated outcome ("reproduced," "could not
reproduce," "reproduced a different but related issue") matches what
the artifacts actually demonstrate. A report claiming success needs an
artifact that actually shows the bug; a report claiming it could not
reproduce needs to show a genuine, complete attempt (full environment
and steps still present) rather than a shrug. Both are acceptable
outcomes; only the mismatch between claim and evidence is the failure.

## Comms

Where it lives: the claim comment and the repro comment (draft or
posted), read against three things: the issue itself (does the
comment name real specifics from it, not boilerplate), the repo's
contribution policy (does it require disclosing AI assistance, and
does the comment comply), and this skill's own voice-guide.md (does
the comment break any personal rule written there).

What good looks like: specific beats generic — the comment references
the actual issue number, symptom, or file, not a template phrase that
could apply to any issue. The claim comment promises investigation and
a report, never a fix or a date. If the repo's policy requires AI-use
disclosure, the comment discloses it plainly rather than omitting it
or hedging around it.