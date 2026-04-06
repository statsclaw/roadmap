# StatsClaw Roadmap

> **Vision**: Input a paper, a conversation, or a set of formulas — get a production-ready statistical package.

StatsClaw is building toward a world where statisticians and econometricians can publish their methods as installable packages without writing boilerplate. This roadmap tracks where we are, what needs fixing now, and where we're headed.

---

## Current Status

**Phase 1 is nearly complete.** The core architecture works: 9 agents, 14 skills, 8 language profiles, brain knowledge-sharing system. But there are critical gaps that block adoption. Those are listed first.

---

## Urgent Fixes — by Apr 9 (all in parallel)

These are things that prevent new users from trying StatsClaw. They must be fixed before anything else.

- [ ] **Hello-world demo** — Add `examples/hello-world/` with a tiny R package + a complete workflow run snapshot. A new user should understand the full workflow in 5 minutes without learning any terminology first.
- [ ] **Julia language profile** — Add `profiles/julia-package.md` (Julia is widely used in statistics: Turing.jl, MLJ.jl, FixedEffectModels.jl). Already tracked in [statsclaw/statsclaw#3](https://github.com/statsclaw/statsclaw/issues/3).
- [ ] **Troubleshooting guide** — Add `docs/TROUBLESHOOTING.md` organized by symptom ("workflow is stuck", "push failed", "agent keeps retrying"), not by internal mechanism.
- [ ] **Stata profile expansion** — Expand `profiles/stata-project.md` to match R profile depth. Stata is core to econometrics — a thin profile means workflows will stall on real Stata tasks.
- [ ] **Cost visibility** — Add a "Cost Summary" section to `templates/log-entry.md` so users can see how many tokens each agent used, how long the workflow took, and how many retries happened.
- [ ] **README update** — Add hello-world link at the top of README.md. Add a "fixed by StatsClaw" badge showing dogfooding count.

**Done when**: A stranger can understand the full StatsClaw workflow in 5 minutes by reading `examples/hello-world/`.

---

## Phase 1: Foundation — by Apr 20

The only Phase 1 item still incomplete is the test suite for the framework itself. Without it, any prompt change can silently break core guarantees like pipeline isolation.

- [ ] **Agent eval harness** — Create `tests/evals/` with 10+ golden test fixtures per agent. Feed each agent a fixed context, check that its output doesn't violate isolation rules (e.g., builder must never reference test-spec). Run on every PR via CI.
- [ ] **Routing regression tests** — Create `tests/routing/fixtures.yml` with 150+ test cases mapping user prompts to expected workflow IDs. Cover Chinese, English, Spanish, and Japanese prompts.
- [ ] **Isolation static checker** — Script that scans all agent definitions and flags if any agent references specs it shouldn't see. Integrate into `validate-structure.sh`.
- [ ] **Dogfooding** — Fix all StatsClaw issues using StatsClaw itself. Push run logs to a public `statsclaw/example-statsclaw-self` workspace repo. This is the best proof that StatsClaw works.
- [x] Multi-pipeline agent architecture (leader, planner, builder, tester, scriber, reviewer, shipper)
- [x] Pipeline isolation (code / test / simulation never see each other's specs)
- [x] 8 language profiles (R, Python, TypeScript, Stata, Go, Rust, C, C++)
- [x] Workspace repo for runtime state and audit trails
- [x] Issue patrol — scan and auto-fix GitHub issues
- [x] Simulation study workflows (Monte Carlo, DGP, coverage)
- [x] CI/CD pipeline for StatsClaw repo
- [x] Brain knowledge-sharing system (distiller agent, brain-sync, privacy-scrub)
- [x] Companion repos: [`statsclaw/brain`](https://github.com/statsclaw/brain), [`statsclaw/brain-seedbank`](https://github.com/statsclaw/brain-seedbank)

**Done when**: CI automatically catches any prompt change that breaks pipeline isolation or routing logic.

---

## Phase 2: Paper-to-Package Pipeline — by Jun 1

This is StatsClaw's killer feature — the reason statisticians will choose it over generic AI coding tools. Other tools can fix bugs and add features; only StatsClaw's three-pipeline architecture can safely turn a paper into a verified package.

- [ ] **LaTeX paper ingestion** — New `skills/paper-ingestion/SKILL.md`. Start with arXiv LaTeX source (structured, most reliable). Planner extracts formulas, algorithm pseudocode, and simulation design. Every extracted formula must carry a `paper-ref` (section + line number) for human verification.
- [ ] **Symbol dictionary in comprehension.md** — Every mathematical symbol in the spec must trace back to the paper. Reviewer checks 100% symbol coverage.
- [ ] **Paper simulation → test-spec + sim-spec** — Map the paper's simulation section (e.g., Table 2) directly into tester acceptance criteria and simulator DGP parameters. This leverages StatsClaw's natural three-spec architecture.
- [ ] **PDF support** — Extend beyond LaTeX to general PDFs.
- [ ] **End-to-end demo** — Take a real arXiv econometrics paper, generate a complete R package with Monte Carlo verification, publish as `statsclaw/example-paper-to-pkg`. Write a blog post.
- [ ] Auto-generate vignettes/tutorials from paper's examples

**Done when**: `build the R package from this arXiv paper <URL>` produces an installable R package that passes Monte Carlo verification end to end.

---

## Phase 3: Interactive Specification — by Jul 15

Move from "one-shot request" to "iterative conversation" — users refine specs through dialogue.

- [ ] Multi-turn conversation mode — leader accumulates context across messages, planner incrementally updates spec.md
- [ ] LaTeX formula input → structured spec generation
- [ ] Visual diagram support (DAGs, model diagrams)
- [ ] Interactive simulation design — choose DGP parameters conversationally
- [ ] Incremental refinement — update package from follow-up papers

---

## Phase 4: Multi-Language & Ecosystem — by Jul 15 (parallel with Phase 3)

- [ ] Cross-language package generation (same estimator → R + Python + Stata simultaneously, with numerical alignment tests to verify both versions produce identical results)
- [ ] CRAN/PyPI/npm/SSC submission automation via shipper
- [ ] Dependency management across ecosystems
- [ ] pkgdown / Quarto documentation site generation

**Done when**: Same estimator ships as both R and Python packages with verified numerical equivalence.

---

## Phase 5: Community & Scale — by Sep 30

- [ ] Plugin architecture — community-contributed profiles and skills, with review process
- [ ] Shared estimator registry — browse and build on existing implementations
- [ ] Brain knowledge expansion — grow the shared knowledge base across domains
- [ ] Brain search improvements — tag-based and semantic search for knowledge entries
- [ ] Brain analytics — track which knowledge entries are most useful
- [ ] Collaborative workflow — multiple contributors on one package
- [ ] Benchmark suite — auto-compare new estimator against existing methods
- [ ] Continuous integration for generated packages

---

## Phase 6: Intelligence — by Dec 31

- [ ] Automatic literature review — find related estimators and compare
- [ ] Numerical stability analysis built into code generation
- [ ] Performance profiling and optimization suggestions
- [ ] Auto-detect edge cases from mathematical properties

---

## Ecosystem Expansion (ongoing, parallel with all phases)

- [ ] **Brain end-to-end validation** — Run 10 real workflows, contribute 10 knowledge entries, verify the full pipeline (extract → privacy scrub → seedbank PR → merge → other users read). These 10 entries become seed content for the brain repo.
- [ ] **Brain tag-based search** — Rebuild `brain/index.md` with tag-based retrieval so leader can find relevant entries at dispatch time.
- [ ] **C/C++ profile expansion** — Deepen to match R profile detail.
- [ ] **Telemetry** — Shipper appends anonymized `run-stats.json` to workspace repo (workflow counts, retry rates, signal frequencies). Aggregated data drives optimization.
- [ ] **Agent development guide** — `docs/AGENT_DEV_GUIDE.md` defining review standards for agent prompt changes.

---

## Promotion Plan

| Date | Milestone | Promotion |
|:-----|:----------|:----------|
| Apr 9 | Hello-world ready | Post to r/statistics, r/econometrics, Hacker News |
| Apr 20 | Eval harness ready | Blog: "How we test an AI agent framework" |
| May 1 | Brain seed knowledge live | Launch "contribute knowledge, earn badges" campaign |
| **Jun 1** | **Paper-to-Package demo** | **Blog + Twitter + EconTwitter — biggest promotion moment** |
| Jul 15 | Cross-language demo | Submit live demo to useR! / PyData / StanCon |
| Monthly | Ongoing | Release notes + brain knowledge newsletter |

**Positioning**: StatsClaw's audit trail + adversarial verification naturally satisfies reproducibility requirements from top journals (AEA, QJE, APSR). This is something no other AI coding tool provides.

---

## Execution Order

```text
Apr 6–9:      [Urgent fixes — all 6 items in parallel]
Apr 10–20:    Phase 1 completion (eval harness + routing tests + isolation checker + dogfooding)
Apr 21–Jun 1: Phase 2 (paper ingestion) ∥ Ecosystem expansion (brain validation + C/C++ profiles)
Jun 2–Jul 15: Phase 3 (interactive) ∥ Phase 4 (cross-language)
Jul 16–Sep 30: Phase 5 (community)
Oct 1–Dec 31: Phase 6 (intelligence)
```

---

## Success Metrics

| Date | Target |
|:-----|:-------|
| Apr 9 | New user can run hello-world in 5 minutes |
| Apr 20 | CI catches isolation violations; 3+ self-repair run logs published |
| Jun 1 | One real arXiv paper → working R package end to end |
| Jul 15 | Same estimator ships as R + Python with numerical alignment |
| Dec 31 | 20+ external contributors, 100+ monthly active users |

---

## How to Influence This Roadmap

This roadmap is community-driven. You can shape it:

- **Feature requests**: [Open an issue](https://github.com/statsclaw/statsclaw/issues/new?template=feature-request.yml) with your idea
- **Paper-to-Package requests**: [Submit a paper](https://github.com/statsclaw/statsclaw/issues/new?template=paper-to-package.yml) you want turned into a package
- **Discussions**: Join the [Ideas discussion board](https://github.com/statsclaw/statsclaw/discussions/categories/ideas) to brainstorm
- **Direct contributions**: See [CONTRIBUTING.md](https://github.com/statsclaw/statsclaw/blob/main/CONTRIBUTING.md) to get started

Every feature request and discussion thread feeds back into this roadmap. We review and prioritize monthly.
