---
name: adversarial-peer-review
description: Use when the user asks to review, critique, stress-test, or evaluate an academic article, dissertation chapter, conference paper, book proposal, or grant application in the humanities or social sciences. Conduct rigorous adversarial peer review by deploying three independent reviewers with distinct critical orientations and synthesising their reports.
version: 1.0.0
author: Nous Research (original Claude skill by Halfofthesky / Elena Pirogova)
license: MIT
platforms: [any]
metadata:
  hermes:
    tags: [academic, peer-review, humanities, adversarial, writing]
    related_skills: [hermes-academic-paper, hermes-academic-reviewer, academic-writing]
---

# Adversarial Peer Review

Conduct rigorous adversarial peer review of humanities scholarship. Three independent reviewers with distinct critical orientations read the submitted text; an editorial synthesis consolidates their reports into a prioritised revision agenda and overall verdict. Designed to surface weaknesses that any single reading perspective would miss.

This is a Hermes port of the Claude skill by [Halfofthesky](https://github.com/Halfofthesky/adversarial-editorial-review). Licensed under MIT.

## When to Use

- User asks to "review", "critique", "stress-test", or "evaluate" an academic text
- User asks for a "peer review", "critical review", "manuscript review", "developmental review"
- User wants to anticipate reviewer objections before submission
- User says "проверь статью", "отрецензируй", "разбери текст"

Scope: literary criticism, intellectual history, cultural studies, political theory, art history, musicology, area studies, philosophy, and adjacent humanities/social-science fields.

Do NOT use for: STEM peer review, book reviews intended for publication, or copyediting.

## Architecture

Three independent reviewers with structurally non-convergent adversarial pressures:

1. **Reviewer 1 — The Evidential Sceptic** — attacks from below: does the material actually support the claims?
2. **Reviewer 2 — The Conceptual Antagonist** — attacks from within: does the argument hold together logically?
3. **Reviewer 3 — The Positional Critic** — attacks from outside: what does the framing make the article unable to see?

The three roles are designed so that fixing what Reviewer 1 finds often does not help with Reviewer 3, and satisfying Reviewer 2's demand for conceptual precision may sharpen exactly the exclusions Reviewer 3 is looking for. This non-convergence is the point — it forces explicit trade-offs.

Full reviewer roles and operating logic: `references/reviewers.md`.
Shared evaluative criteria all reviewers use: `references/methodology.md`.
Editorial synthesis, rebuttal, and revision tracking: `references/synthesis.md`.
Prose diagnostics and bibliographic checking: `references/diagnostics.md`.

## Workflow

### Step 1: Determine parameters

Before reviewing, establish three things. If the text does not make them clear, ask the user.

**Genre:** journal article, dissertation chapter, conference paper, book proposal, or grant application. Default to journal article standards if ambiguous, but note the assumption.

**Discipline:** literary criticism, history, political theory, cultural studies, area studies, philosophy, musicology, art history, or other. If unclear, ask.

**Severity:**
- **Developmental** — work in progress; constructive tone; revision suggestions included.
- **Standard** — honest journal-level assessment; revision suggestions included. (Default.)
- **Stress-test** — assume hostile reviewers; flag every exploitable weakness; omit revision suggestions; include simulated author's rebuttal.

### Step 2: Run three independent adversarial reviews

Produce three reviews, one per role. Each reviewer works independently — do not let one reviewer's concerns contaminate another's analysis. Each applies the shared methodology through their own adversarial lens.

For very long texts (15,000+ words), suggest submitting in sections.

**Output format for each reviewer (in order):**

- **Verdict** — single sentence.
- **Primary concern** — the single most serious problem; if left unaddressed, most undermines the text's contribution.
- **Secondary concerns** — numbered list of 3–6 additional problems, ranked by severity. Each item is a full paragraph: state the problem, locate it in the text, explain why it matters. Do not pad with trivial complaints.
- **Strengths** — one paragraph tied to concrete features. Even a severely flawed text has strengths; identifying them is part of honest assessment, not politeness.
- **Revision suggestions** (Developmental and Standard only; omit at Stress-test) — concrete, actionable recommendations.

Integrate prose diagnostics and bibliographic check findings into the relevant sections rather than reporting them separately. See `references/diagnostics.md`.

### Step 3: Editorial synthesis

After all three reviews, produce the synthesis (see `references/synthesis.md`):

- **Convergence** — concerns raised by two or more reviewers.
- **Divergence** — disagreements, with explanation and recommendation.
- **Prioritised revision agenda** — numbered, most urgent first. Each item: problem statement, which reviewer(s) raised it, revision type, scale estimate (minor / moderate / major).
- **Overall assessment** — accept with minor revisions / revise and resubmit / major revision required / reject (or "Rethink and restart" at Developmental severity).

### Step 4: Author's rebuttal (optional)

Simulated author's response showing which objections are survivable and which are structural. Each concern classified as *accepted*, *partially accepted*, or *rebutted*, followed by residual vulnerabilities. See `references/synthesis.md`.

- Include by default at **Stress-test** severity.
- **Ask** at **Standard** severity.
- **Omit** at **Developmental** severity.

### Step 5: Revision tracking (if applicable)

If the user submits a revised version, compare each concern from the prior review against the new text. Classify as *fully addressed*, *partially addressed*, *not addressed*, or *introduced new problem*. Present as a tracking table followed by an updated synthesis.

## Formatting

Use markdown. Section headers: `## Reviewer 1: The Evidential Sceptic`, `## Reviewer 2: The Conceptual Antagonist`, `## Reviewer 3: The Positional Critic`, `## Editorial Synthesis`, `## Author's Rebuttal`.

Within each review: `### Verdict`, `### Primary concern`, `### Secondary concerns`, `### Strengths`, `### Revision suggestions`.

Do not use bullet points inside paragraph body text. Secondary concerns use a numbered list, but each item is a full paragraph, not a bullet.

## Tone

Adversarial does not mean hostile. Each reviewer is rigorous, direct, and unsparing, but never contemptuous. The goal is to make the scholarship better, not to perform cleverness at the author's expense. Even at Stress-test severity, the tone is that of a demanding but fair colleague, not a bully.

## Hermes-specific notes

- For parallel execution: the three reviews can be delegated as sub-tasks via `delegate_task` if context limits are a concern. Each sub-agent receives the full text + one reviewer role definition + the methodology reference.
- The editorial synthesis must run in the parent session after all three reviews are collected — it needs all three outputs.
- Prose diagnostics (`references/diagnostics.md`) are performed inline during each review, not as a separate pass.
- The `references/` directory contains the full reviewer definitions, methodology, synthesis procedures, and diagnostic procedures — load them before starting the review.

## Common Pitfalls

1. **Reviewer contamination.** Each reviewer writes as if they haven't read the other reports. Don't let Reviewer 2 reference Reviewer 1's concerns.
2. **Fake convergence.** Don't artificially make reviewers agree. Structural non-convergence is the point — it shows the author which trade-offs they must make.
3. **Padding.** Don't add trivial complaints to reach a target number of secondary concerns. Fewer, sharper concerns are better.
4. **Missing diagnostics.** Integrate prose diagnostics and bibliographic checks — don't skip them just because the prose "seems fine."
5. **Wrong severity tone.** Stress-test omits revision suggestions entirely. Developmental softens "reject" to "Rethink and restart."
6. **Forgetting the synthesis.** The three reviews alone are not the deliverable. The editorial synthesis that reconciles them is the actual output.

## Verification Checklist

- [ ] Parameters (genre, discipline, severity) established
- [ ] All three reviews completed with correct structure
- [ ] Each reviewer operates independently (no cross-contamination)
- [ ] Prose diagnostics and bibliographic check integrated into reviews
- [ ] Editorial synthesis: convergence, divergence, prioritised agenda, overall verdict
- [ ] Author's rebuttal included per severity rules
- [ ] Formatting: markdown headers, no bullet points in body paragraphs