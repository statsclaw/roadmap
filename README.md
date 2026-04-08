# StatsClaw Roadmap

> StatsClaw helps researchers build statistical packages with AI agent teams. This roadmap tracks what we're working on and where we think the project should go. Priorities shift as we learn.

---

## Where We Are

StatsClaw is an early-stage framework. The core agent architecture works — 9 agents with pipeline isolation, 8 language profiles, a set of skills and templates. We've used it to build a few example packages ([probit](https://github.com/statsclaw/example-probit), [R2PY](https://github.com/statsclaw/example-R2PY), [fect](https://github.com/statsclaw/example-fect), [panelView](https://github.com/statsclaw/example-panelView)), and those are the best evidence of what it can and can't do today.

What's missing is a lot. There are no automated tests for the framework itself, no easy onboarding path for new users, and some language profiles are too thin to handle real workflows. The shared knowledge system (brain) exists as infrastructure but has no content yet.

---

## Near-Term: Onboarding & Stability

These are practical blockers that make it hard for anyone to try StatsClaw today.

- [ ] **Hello-world demo** — A small, self-contained example someone can run in 5 minutes. `examples/hello-world/`.
- [ ] **Troubleshooting guide** — `docs/TROUBLESHOOTING.md`, organized by symptom.
- [ ] **Stata profile expansion** — The current profile is much thinner than R's. Real Stata workflows will run into gaps.
- [ ] **Julia language profile** — Julia is widely used in statistics and we don't support it yet. [statsclaw/statsclaw#3](https://github.com/statsclaw/statsclaw/issues/3).
- [ ] **Cost visibility** — Show users what each run costs. Add a cost summary section to run logs.
- [ ] **README update** — Link to hello-world, clarify what the project actually does vs. what's planned.

---

## Self-Testing

There are no automated tests for StatsClaw itself right now. A bad prompt edit can silently break the framework.

- [ ] **Agent smoke tests** — Feed each agent a fixed input, verify it produces reasonable output and doesn't leak across pipelines.
- [ ] **Routing tests** — A set of example prompts mapped to expected workflows. Catches misrouting.
- [ ] **Isolation checker** — Verify no agent can access specs it shouldn't. Run in CI.
- [ ] **Dogfooding** — Use StatsClaw to work on StatsClaw's own issues. Publish the run logs so people can see what actually happens.

---

## Exploring: Paper-to-Package

StatsClaw can already work from uploaded files and conversation to produce specs. We'd like to go further — structured ingestion of academic papers, tracing formulas back to source, mapping simulation designs to specs.

This is harder than it sounds. PDF and LaTeX parsing is a deep problem, and "paper → installable package" involves a lot of judgment calls that still need researcher involvement. We're working on it but not making promises about timelines.

- [ ] **LaTeX paper ingestion** — Start with arXiv LaTeX. Track where each formula comes from.
- [ ] **Symbol tracing** — Every symbol in the spec should map back to the paper.
- [ ] **Simulation mapping** — Try to connect paper simulation sections to spec parameters.
- [ ] **PDF support** — Broaden beyond LaTeX sources.
- [ ] **End-to-end example** — If we get this working well enough, publish a real paper-to-package case study.

---

## Exploring: Deeper Interactive Specification

The framework already handles multi-turn conversations and iterative refinement. Areas we'd like to improve:

- [ ] **LaTeX formula input** — Let users paste formulas and get structured specs.
- [ ] **Interactive simulation design** — Let users tweak DGP parameters conversationally.
- [ ] **Incremental refinement** — Update a package from follow-up work without starting over.

---

## Longer-Term Ideas

These are things we think would be valuable but haven't started on. Some may turn out to be impractical.

- [ ] **Automatic related-work comparison** — Find related estimators and show how they compare. This is essentially a literature search problem and we don't know yet how well it can work.
- [ ] **Numerical stability analysis** — Flag potential stability issues during code generation.
- [ ] **Performance profiling suggestions** — Point out obvious bottlenecks in generated code.

---

## Infrastructure (as needed)

We'll build these when there's actual demand, not before.

- [ ] **Brain content** — The shared knowledge system needs actual entries before we invest in search, analytics, or community features. First priority is getting a few real knowledge entries from our own workflows.
- [ ] **C/C++ profile expansion** — Bring it closer to R profile depth when someone needs it.
- [ ] **Agent development guide** — Document how to review and modify agent prompts safely.
- [ ] **CI for generated packages** — Automated checks on packages StatsClaw produces.

---

## What We're Not Doing Yet

Some things that appeared in earlier versions of this roadmap but are premature:

- **Plugin architecture / estimator registry** — There's no community to serve yet. We'll revisit when there is.
- **Brain search / analytics / badges** — The brain has no content. Infrastructure for empty systems is wasted effort.
- **Conference submissions** — The project isn't mature enough. When it is, the work will speak for itself.
- **Benchmark suites** — Useful eventually, but we need more working examples first.

---

## How We Think About Progress

The best thing we can do right now is **produce more high-quality examples**. The probit package shows the framework can build something from a spec. The R2PY translation shows it can handle a larger scope. But we need examples with enough complexity that a working statistician looks at them and thinks "this actually saved me real time."

Pipeline isolation — where build, test, and simulation agents can't see each other's specs — is the core architectural idea. When three independent pipelines converge on the same answer, that's meaningful. But the idea needs more evidence behind it, not more marketing in front of it.

---

## How to Influence This Roadmap

- **Feature requests**: [Open an issue](https://github.com/statsclaw/statsclaw/issues/new?template=feature-request.yml)
- **Paper-to-Package requests**: [Submit a paper](https://github.com/statsclaw/statsclaw/issues/new?template=paper-to-package.yml)
- **Discussions**: [Ideas board](https://github.com/statsclaw/statsclaw/discussions/categories/ideas)
- **Contribute**: [CONTRIBUTING.md](https://github.com/statsclaw/statsclaw/blob/main/CONTRIBUTING.md)
