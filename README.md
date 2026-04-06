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

**Problem**: Any prompt edit can silently break pipeline isolation, routing, or agent behavior. There are no automated tests for the framework itself.

- [ ] **Agent eval harness** — `tests/evals/` with 10+ golden fixtures per agent. Builder must never see test-spec. Tester must never see spec. Run on every PR.
- [ ] **Routing regression tests** — `tests/routing/fixtures.yml` with 150+ prompt→workflow mappings. Chinese, English, Spanish, Japanese.
- [ ] **Isolation static checker** — Script that scans agent definitions for cross-pipeline spec references. Integrated into CI.
- [ ] **Dogfooding** — Fix all StatsClaw issues using StatsClaw. Publish run logs to `statsclaw/example-statsclaw-self`.

**Done when**: CI blocks any PR that breaks pipeline isolation or misroutes a prompt.

---

## Phase 2: Paper-to-Package — Apr 17–30

**Problem**: StatsClaw's killer feature doesn't exist yet. No other tool can turn a paper into a verified package — but StatsClaw can't either, today.

- [ ] **LaTeX paper ingestion** — `skills/paper-ingestion/SKILL.md`. arXiv LaTeX first. Every formula carries `paper-ref` (section + line) for traceability.
- [ ] **Symbol dictionary** — Every symbol in the spec traces back to the paper. Reviewer checks 100% coverage.
- [ ] **Paper simulation → specs** — Map Table 2 directly into `test-spec.md` acceptance criteria and `sim-spec.md` DGP parameters.
- [ ] **PDF support** — General PDFs beyond LaTeX.
- [ ] **End-to-end demo** — Real arXiv paper → installable R package with Monte Carlo verification. Published as `statsclaw/example-paper-to-pkg`. Blog post.
- [ ] **Auto-generate vignettes** from paper examples.

**Done when**: `"build the R package from this arXiv paper"` produces an installable, verified R package end to end.

---

## Phase 3: Interactive Specification — May 1–14

**Problem**: Users must specify everything in one shot. Complex packages need back-and-forth refinement — especially when translating math into code.

- [ ] **Multi-turn conversation** — Leader accumulates context, planner incrementally updates spec.md.
- [ ] **LaTeX formula input** → structured spec generation.
- [ ] **Visual diagram support** — DAGs, model diagrams.
- [ ] **Interactive simulation design** — Choose DGP parameters conversationally.
- [ ] **Incremental refinement** — Update package from follow-up papers.

**Done when**: A user can refine an estimator spec across 5+ conversation turns without restarting.

---

## Phase 4: Multi-Language Shipping — May 1–14 (parallel with Phase 3)

**Problem**: Statisticians need packages in R, Python, AND Stata. Today StatsClaw generates one language at a time with no cross-language verification.

- [ ] **Cross-language generation** — Same estimator → R + Python + Stata simultaneously. Numerical alignment tests verify identical results.
- [ ] **Submission automation** — CRAN / PyPI / npm / SSC via shipper.
- [ ] **Cross-ecosystem dependency management**.
- [ ] **Documentation site generation** — pkgdown / Quarto.

**Done when**: Same estimator ships as R + Python packages with verified numerical equivalence.

---

## Phase 5: Community — May 15–31

**Problem**: StatsClaw is a solo project. Scaling requires community contributions — profiles, skills, estimator implementations, knowledge entries.

- [ ] **Plugin architecture** — Community-contributed profiles and skills with review process.
- [ ] **Estimator registry** — Browse and build on existing implementations.
- [ ] **Brain expansion** — Grow shared knowledge across domains.
- [ ] **Brain search** — Tag-based and semantic retrieval.
- [ ] **Brain analytics** — Track which entries are most useful.
- [ ] **Collaborative workflow** — Multiple contributors on one package.
- [ ] **Benchmark suite** — Auto-compare new estimator against existing methods.
- [ ] **CI for generated packages**.

**Done when**: 5+ community-contributed profiles or skills merged via PR.

---

## Phase 6: Intelligence — Jun 1–15

**Problem**: Users still need to know which estimators exist and how theirs compares. StatsClaw should find this automatically.

- [ ] **Automatic literature review** — Find related estimators and compare.
- [ ] **Numerical stability analysis** built into code generation.
- [ ] **Performance profiling** and optimization suggestions.
- [ ] **Edge case detection** from mathematical properties.

**Done when**: StatsClaw auto-generates a "related work" comparison table for any new estimator.

---

## Ecosystem Track (ongoing, parallel with all phases)

- [ ] **Brain end-to-end validation** — 10 real workflows → 10 knowledge entries → full pipeline verified.
- [ ] **Brain tag-based search** — Rebuild `brain/index.md` with proper retrieval.
- [ ] **C/C++ profile expansion** — Match R profile depth.
- [ ] **Telemetry** — `run-stats.json` in workspace repo (counts, retries, signal frequencies).
- [ ] **Agent development guide** — `docs/AGENT_DEV_GUIDE.md` for prompt change review standards.

---

## Execution Order

```text
Apr 6–9:    Phase 0 — adoption blockers (all 6 in parallel)
Apr 10–16:  Phase 1 — self-testing (eval + routing + isolation + dogfooding)
Apr 17–30:  Phase 2 — paper-to-package ∥ ecosystem track
May 1–14:   Phase 3 (interactive) ∥ Phase 4 (cross-language)
May 15–31:  Phase 5 — community
Jun 1–15:   Phase 6 — intelligence
```

---

## Promotion Plan

| Date | Milestone | Action |
|:-----|:----------|:-------|
| Apr 9 | Hello-world ships | Post to r/statistics, r/econometrics, Hacker News |
| Apr 16 | Eval harness live | Blog: "How we test an AI agent framework" |
| Apr 30 | **Paper-to-Package demo** | **Blog + Twitter + EconTwitter — biggest moment** |
| May 14 | Cross-language demo | Submit to useR! / PyData / StanCon |
| May 31 | Community launch | "Contribute a profile" campaign |
| Monthly | Ongoing | Release notes + brain knowledge newsletter |

**Positioning**: StatsClaw's audit trail + adversarial verification satisfies reproducibility requirements from top journals (AEA, QJE, APSR). No other AI coding tool does this.

---

## Success Metrics

| Date | Target |
|:-----|:-------|
| Apr 9 | New user runs hello-world in 5 minutes |
| Apr 16 | CI blocks isolation-breaking PRs |
| Apr 30 | One arXiv paper → verified R package end to end |
| May 14 | Same estimator ships as R + Python |
| Jun 15 | 10+ external contributors |

---

## How to Influence This Roadmap

- **Feature requests**: [Open an issue](https://github.com/statsclaw/statsclaw/issues/new?template=feature-request.yml)
- **Paper-to-Package requests**: [Submit a paper](https://github.com/statsclaw/statsclaw/issues/new?template=paper-to-package.yml)
- **Discussions**: [Ideas board](https://github.com/statsclaw/statsclaw/discussions/categories/ideas)
- **Contribute**: [CONTRIBUTING.md](https://github.com/statsclaw/statsclaw/blob/main/CONTRIBUTING.md)
