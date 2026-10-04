# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

### Who I am in threads

I'm a newcomer making my first open source contribution. I'm comfortable
with Python and have used Java and JavaScript on past projects, but I
have no track record in this specific codebase yet. Readers should
expect careful, incremental updates from me — I will say exactly what
I've verified and what I haven't, and I'll ask before assuming.

## Rules I write by

### Rule: Never promise a fix or a date

A claim comment promises investigation and a report, not a solved
problem or a timeline. I don't know yet how hard the real fix will be,
so I don't commit to one before I've even reproduced the bug.

- Wrong: "I'll have a PR up fixing this by this weekend!"
- Right: "I'm going to set up the environment and reproduce this issue,
  and I'll report back with what I find."

### Rule: Name the specific issue, never a template line

If my comment could be pasted onto any issue in any repo without
editing a word, it's not specific enough to be useful.

- Wrong: "Looking into this, will update soon!"
- Right: "Claiming issue #36 — I'll add a test case for the
  no-ingested-documents path in test_review_routes.py and report what
  I find."

### Rule: State uncertainty plainly instead of hedging around it

If I'm not sure whether something reproduced, or whether I understood
the issue correctly, I say that directly rather than implying more
confidence than I have.

- Wrong: "This seems to be working as expected now I think, might be
  fixed?"
- Right: "I was not able to reproduce the described error following
  these exact steps: [steps]. I may be missing a setup step — flagging
  this rather than assuming it's resolved."

### Rule: Disclose AI assistance when the repo's policy asks for it

If a repo's contribution policy requires saying when AI tools helped,
I say so plainly, in the comment itself, not buried in a PR description
or omitted because it feels awkward.

- Wrong: [no mention of AI tools at all, on a repo whose CONTRIBUTING.md
  requires disclosure]
- Right: "I used Claude Code to help set up my environment and review
  my reproduction steps; the findings below are my own verified work."

### Rule: Keep the comment proportionate to what I actually did

I don't pad a short investigation to look more thorough, and I don't
compress a real, multi-step investigation into one vague line.

- Wrong: "Did a deep investigation into the root cause and several
  contributing factors across the codebase." (for a 10-minute check)
- Right: "Ran the existing test suite and reproduced the missing-case
  error in two lines of output — details below."

## Things I never post

- A promise of a specific fix date or PR timeline before I've reproduced
  the issue.
- "Same as above, can confirm" or any other piggyback on someone else's
  reproduction — my proof is always my own words, from my own
  environment.
- A claim of success ("fixed!", "reproduced!") without the actual
  artifact (output, log, screenshot) attached to back it up.
- Omitting AI-assistance disclosure when a repo's policy requires it,
  even if it feels like it undersells my own understanding.