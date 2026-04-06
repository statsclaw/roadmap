# StatsClaw Roadmap

> **Vision**: Input a paper, a conversation, or a set of formulas — get a production-ready statistical package.

---

## Current Status

The core architecture is built: 9 agents, 14 skills, 8 language profiles, brain knowledge-sharing. What's missing is everything that turns this from a working prototype into something people actually use.

---

## Phase 0: Adoption Blockers — Apr 6–9

**Problem**: Nobody can try StatsClaw today. There's no demo, no troubleshooting guide, and key profiles are too thin to work on real projects.

- [ ] **Hello-world demo** — `examples/hello-world/` with a tiny R package + complete workflow snapshot. 5 minutes to understand, zero terminology.
- [ ] **Julia language profile** — `profiles/julia-package.md`. Julia is everywhere in statistics. [statsclaw/statsclaw#3](https://github.com/statsclaw/statsclaw/issues/3).
- [ ] **Troubleshooting guide** — `docs/TROUBLESHOOTING.md`. Organized by symptom, not internals.
- [ ] **Stata profile expansion** — Current profile is 2.2 KB vs R's 8.5 KB. Real Stata workflows will stall.
- [ ] **Cost visibility** — "Cost Summary" section in `templates/log-entry.md`. Users need to know what each run costs.
- [ ] **README update** — Hello-world link at top. Dogfooding badge.

**Done when**: A stranger runs the full workflow in 5 minutes from the hello-world example.

---

## Phase 1: Self-Testing — Apr 10–16

**Problem**: There are no automated tests for StatsClaw itself. A bad prompt edit can silently break the whole framework and nobody would know until a real workflow fails.

- [ ] **Agent tests** — Feed each agent a fixed input, check it produces correct output and doesn't leak across pipelines. 10+ test cases per agent, runs on every PR.
- [ ] **Routing tests** — 150+ example prompts (multi-language) mapped to expected workflows. Catches misrouting before it ships.
- [ ] **Isolation checker** — Script that verifies no agent can see specs it shouldn't. Runs in CI.
- [ ] **Dogfooding** — Use StatsClaw to fix StatsClaw's own issues. Publish the run logs as proof it works.

**Done when**: CI catches broken prompts automatically.

---

## Phase 2: Paper-to-Package — Apr 17–30

**Problem**: StatsClaw can already ingest uploaded files and produce specs from them. What's missing is structured paper ingestion — tracing every formula back to the source, mapping simulation sections to specs automatically, and handling raw PDFs.

- [ ] **LaTeX paper ingestion** — `skills/paper-ingestion/SKILL.md`. arXiv LaTeX first. Every formula carries `paper-ref` (section + line) for traceability.
- [ ] **Symbol dictionary** — Every symbol in the spec traces back to the paper. Reviewer checks 100% coverage.
- [ ] **Paper simulation → specs** — Map Table 2 directly into `test-spec.md` acceptance criteria and `sim-spec.md` DGP parameters.
- [ ] **PDF support** — General PDFs beyond LaTeX.
- [ ] **End-to-end demo** — Real arXiv paper → installable R package with Monte Carlo verification. Published as `statsclaw/example-paper-to-pkg`. Blog post.
- [ ] **Auto-generate vignettes** from paper examples.

**Done when**: `"build the R package from this arXiv paper"` produces an installable, verified R package end to end.

---

## Phase 3: Interactive Specification — May 1–14

**Problem**: StatsClaw already handles multi-turn conversations and iterative refinement. What needs deepening: structured LaTeX formula input, visual diagram support, and conversational simulation design where users tweak DGP parameters interactively.

- [ ] **LaTeX formula input** → structured spec generation.
- [ ] **Visual diagram support** — DAGs, model diagrams.
- [ ] **Interactive simulation design** — Choose DGP parameters conversationally.
- [ ] **Incremental refinement** — Update package from follow-up papers.

**Done when**: A user can input LaTeX formulas and refine DGP parameters conversationally across multiple turns.

---

## Phase 4: Intelligence — May 15–31

**Problem**: Users still need to know which estimators exist and how theirs compares. StatsClaw should find this automatically.

- [ ] **Automatic literature review** — Find related estimators and compare.
- [ ] **Numerical stability analysis** built into code generation.
- [ ] **Performance profiling** and optimization suggestions.
- [ ] **Edge case detection** from mathematical properties.

**Done when**: StatsClaw auto-generates a "related work" comparison table for any new estimator.

---

## Community (ongoing since Mar 30, parallel with all phases)

Community building is not a phase — it runs continuously alongside everything else.

- [ ] **Plugin architecture** — Community-contributed profiles and skills with review process.
- [ ] **Estimator registry** — Browse and build on existing implementations.
- [ ] **Brain expansion** — Grow shared knowledge across domains.
- [ ] **Brain search** — Tag-based and semantic retrieval.
- [ ] **Brain analytics** — Track which entries are most useful.
- [ ] **Collaborative workflow** — Multiple contributors on one package.
- [ ] **Benchmark suite** — Auto-compare new estimator against existing methods.
- [ ] **CI for generated packages**.

---

## Ecosystem Track (ongoing, parallel with all phases)

- [ ] **Brain end-to-end validation** — 10 real workflows → 10 knowledge entries → full pipeline verified.
- [ ] **C/C++ profile expansion** — Match R profile depth.
- [ ] **Telemetry** — `run-stats.json` in workspace repo (counts, retries, signal frequencies).
- [ ] **Agent development guide** — `docs/AGENT_DEV_GUIDE.md` for prompt change review standards.
- [ ] **Registry submission automation** — CRAN / PyPI / SSC submission via shipper. Profiles already handle multi-language; this adds the last-mile publish step.

---

## Execution Order

```text
Ongoing:    Community building + ecosystem track (started Mar 30)
Apr 6–9:    Phase 0 — adoption blockers (all 6 in parallel)
Apr 10–16:  Phase 1 — self-testing (eval + routing + isolation + dogfooding)
Apr 17–30:  Phase 2 — paper-to-package
May 1–14:   Phase 3 — deepen interactive specification
May 15–31:  Phase 4 — intelligence
```

---

## Promotion Plan

| Date | Milestone | Action |
|:-----|:----------|:-------|
| Apr 9 | Hello-world ships | Post to r/statistics, r/econometrics, Hacker News |
| Apr 16 | Eval harness live | Blog: "How we test an AI agent framework" |
| Apr 30 | **Paper-to-Package demo** | **Blog + Twitter + EconTwitter — biggest moment** |
| May 14 | Interactive deepening done | Demo: conversational simulation design |
| May 31 | Intelligence features | Submit demo to useR! / PyData / StanCon |
| Monthly | Ongoing | Release notes + community highlights + brain newsletter |

**Positioning**: StatsClaw's audit trail + adversarial verification satisfies reproducibility requirements from top journals (AEA, QJE, APSR). No other AI coding tool does this.

---

## Success Metrics

| Date | Target |
|:-----|:-------|
| Apr 9 | New user runs hello-world in 5 minutes |
| Apr 16 | CI blocks isolation-breaking PRs |
| Apr 30 | One arXiv paper → verified R package end to end |
| May 14 | LaTeX formula input + conversational DGP design working |
| May 31 | Auto-generated "related work" table for any new estimator |

---

## How to Influence This Roadmap

- **Feature requests**: [Open an issue](https://github.com/statsclaw/statsclaw/issues/new?template=feature-request.yml)
- **Paper-to-Package requests**: [Submit a paper](https://github.com/statsclaw/statsclaw/issues/new?template=paper-to-package.yml)
- **Discussions**: [Ideas board](https://github.com/statsclaw/statsclaw/discussions/categories/ideas)
- **Contribute**: [CONTRIBUTING.md](https://github.com/statsclaw/statsclaw/blob/main/CONTRIBUTING.md)
