<div align="center">

# 📝 Adversarial Editorial Review

![Hermes](https://img.shields.io/badge/Hermes-Agent-6366f1?style=for-the-badge&logo=robot&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-Skill-d97706?style=for-the-badge&logo=anthropic&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)

**Rigorous adversarial peer review of humanities scholarship — three independent reviewers, one editorial synthesis**

</div>

> Three independent reviewers with distinct critical orientations read your text. An editorial synthesis consolidates their reports into a prioritised revision agenda. Designed to surface weaknesses that any single reading perspective would miss. Hermes port of the original Claude skill by [Halfofthesky](https://github.com/Halfofthesky/adversarial-editorial-review).

<div align="center">
  <a href="#-quick-start">Quick Start</a> · <a href="#-features">Features</a> · <a href="#-architecture">Architecture</a> · <a href="#-roadmap">Roadmap</a>
</div>

---

## 💡 Concept

Traditional peer review gives you one reader's perspective. This skill gives you three — each with a structurally different adversarial orientation. The Evidential Sceptic attacks your evidence, the Conceptual Antagonist attacks your logic, and the Positional Critic attacks your framing. Their concerns are designed to be non-convergent: fixing what one finds often worsens another's complaint. This forces explicit trade-offs instead of a flat list of fixes. An editorial meta-reviewer then synthesises all three reports into a prioritised revision agenda with an overall verdict.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| Three adversarial reviewers | Evidential Sceptic, Conceptual Antagonist, Positional Critic — each with distinct epistemic stance and operating question |
| Editorial synthesis | Convergence/divergence analysis + prioritised revision agenda + overall assessment |
| Three severity levels | Developmental (constructive), Standard (journal-level), Stress-test (hostile reviewers) |
| Prose diagnostics | Jargon density, assertion-to-evidence ratio, hedging patterns, sentence length variation, passive voice concentration |
| Bibliographic check | Cited-but-not-discussed, discussed-but-not-cited, internal inconsistencies, obvious absences, citational politics |
| Author's rebuttal | Simulated author response — which objections are survivable, which are structural |
| Revision tracking | Compare revised text against previous review: fully/partially/not addressed + new problems |
| Genre-aware | Calibrated for journal articles, dissertation chapters, conference papers, book proposals, and grant applications |

---

## 🚀 Quick Start

### Install in Hermes

```bash
# Copy the skill into your Hermes skills directory
cp -r skills/adversarial-peer-review ~/.hermes/skills/
```

Or on Windows:

```powershell
xcopy /E skills\adversarial-peer-review %USERPROFILE%\.hermes\skills\adversarial-peer-review\
```

### Usage

Attach or paste the text, then ask naturally:

- *"Review this article."*
- *"Stress-test this before I submit to Modern Language Review."*
- *"Give me a developmental review of this dissertation chapter."*
- *"This is a revised version — compare against the previous review."*

The skill asks for missing parameters (genre, discipline, severity), then produces three independent reviews, an editorial synthesis, and — at Stress-test severity — a simulated author's rebuttal.

<details>
<summary>⚙️ Severity Levels</summary>

- **Developmental** — constructive, forward-looking; for works in progress
- **Standard** (default) — honest, journal-level assessment
- **Stress-test** — assume hostile reviewers and flag every exploitable weakness

</details>

---

## 🏗️ Architecture

| Reviewer | Target | Epistemic Stance | Operating Question |
|----------|--------|------------------|-------------------|
| Reviewer 1 — Evidential Sceptic | Empirical foundation | Evidence is weaker than claimed until proven otherwise | *Does the material actually support what the author claims?* |
| Reviewer 2 — Conceptual Antagonist | Intellectual architecture | Argument contains a hidden flaw until proven otherwise | *Does the argument actually hold together?* |
| Reviewer 3 — Positional Critic | The frame itself | Framing is narrower than acknowledged until proven otherwise | *What does the article's own framing make it unable to see?* |

The three reviewers' concerns are structurally non-convergent by design. Satisfying Reviewer 2's demand for conceptual precision may sharpen exactly the exclusions Reviewer 3 is looking for. This tension is productive — it shows the author which trade-offs they must make.

<details>
<summary>📁 Skill Structure</summary>

```
adversarial-peer-review/
├── SKILL.md                          # Main skill: workflow, formatting, tone
└── references/
    ├── methodology.md                # Shared evaluative criteria
    ├── reviewers.md                  # Three reviewer roles and logic
    ├── synthesis.md                  # Editorial synthesis + rebuttal + tracking
    └── diagnostics.md               # Prose diagnostics + bibliographic check
```

</details>

---

## 🗺️ Roadmap

- [x] Hermes skill port (SKILL.md + 4 reference files)
- [x] GitHub repo with README, llms.txt, llms-full.txt
- [ ] Hermes plugin wrapper (/review slash command)
- [ ] Sample review output in `examples/`
- [ ] CI validation for skill structure
- [ ] Upstream PR: offer Hermes compatibility layer to Halfofthesky/adversarial-editorial-review

---

## 🤝 Contributing

Fork → `feature/name` → PR

This is a Hermes port of [Halfofthesky/adversarial-editorial-review](https://github.com/Halfofthesky/adversarial-editorial-review) (MIT). Issues and PRs welcome. For substantive changes to reviewer roles or methodology, open an issue first.

---

## 📄 License

[Maxim Osovsky](https://www.linkedin.com/in/maximosovsky/). Licensed under [MIT](https://opensource.org/licenses/MIT) — same as upstream.