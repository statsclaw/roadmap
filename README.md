# StatsClaw Roadmap

> StatsClaw helps researchers build statistical packages with AI agent teams. This roadmap tracks what we're working on next.

---

## Where We Are

StatsClaw is an early-stage framework. The core agent architecture works — 9 agents with pipeline isolation, 8 language profiles, a set of skills and templates. We've used it to build a few packages ([probit](https://github.com/statsclaw/example-probit), [R2PY](https://github.com/statsclaw/example-R2PY)) and contribute to existing ones ([fect](https://github.com/statsclaw/example-fect), [panelView](https://github.com/statsclaw/example-panelView)). Those examples are the best way to judge what it can do today.

There's a lot still missing: no automated tests for the framework itself, no easy onboarding path, some language profiles are too thin for real work, and the shared knowledge system (brain) has very little content so far.

---

## Phase 0: Adoption Blockers — Apr 8–14

Making it possible for someone outside the team to actually try StatsClaw.

- [ ] **Hello-world demo** — `examples/hello-world/` with a small R package and a complete workflow snapshot.
- [ ] **Julia language profile** — `profiles/julia-package.md`. [statsclaw/statsclaw#3](https://github.com/statsclaw/statsclaw/issues/3).
- [ ] **Troubleshooting guide** — `docs/TROUBLESHOOTING.md`. Organized by symptom.
- [ ] **Stata profile expansion** — Current profile is much thinner than R's. Needs work before real Stata workflows.
- [ ] **Cost visibility** — Show what each run costs in the run log.
- [ ] **README update** — Link to hello-world, clarify what's working vs. what's planned.

---

## Phase 1: Self-Testing — Apr 15–25

A bad prompt edit can silently break the framework. We need basic regression coverage.

- [ ] **Agent smoke tests** — Feed each agent a fixed input, check it produces reasonable output and doesn't leak across pipelines.
- [ ] **Routing tests** — Example prompts mapped to expected workflows. Catches misrouting.
- [ ] **Isolation checker** — Verify no agent can access specs it shouldn't. Run in CI.
- [ ] **Dogfooding** — Use StatsClaw to work on StatsClaw's own issues. Publish the run logs.

---

## Phase 2: Paper-to-Package — Apr 25 – May 15

StatsClaw can already work from uploaded files and conversation. We want to improve structured paper ingestion — but this is a hard problem and we're approaching it incrementally.

- [ ] **LaTeX paper ingestion** — Start with arXiv LaTeX. Track where each formula comes from (`paper-ref`).
- [ ] **Symbol tracing** — Every symbol in the spec should map back to the paper.
- [ ] **Simulation mapping** — Connect paper simulation sections to spec parameters where possible.
- [ ] **PDF support** — Broaden beyond LaTeX sources.
- [ ] **Case study** — If this works well enough, publish a real paper-to-package example.

"Paper → installable package" involves many judgment calls that still need researcher involvement. We're exploring how far automation can go, not promising a fully hands-off pipeline.

---

## Phase 3: Interactive Specification — May 15–31

The framework handles multi-turn conversation and iterative refinement. Areas we'd like to improve:

- [ ] **LaTeX formula input** — Let users paste formulas and get structured specs.
- [ ] **Interactive simulation design** — Tweak DGP parameters conversationally.
- [ ] **Incremental refinement** — Update a package from follow-up work without starting over.

---

## Longer-Term Ideas

Things we think could be valuable but haven't started. Some may turn out to be impractical.

- [ ] **Related-work comparison** — Surface related estimators during planning. This is essentially a literature search problem; we don't know how well it can work yet.
- [ ] **Numerical stability flags** — Warn about potential stability issues during code generation.
- [ ] **Performance suggestions** — Point out obvious bottlenecks in generated code.

---

## Infrastructure (ongoing, as needed)

We'll build these when there's real demand.

- [ ] **Brain content** — The knowledge system needs real entries before we invest in search or analytics. First priority: populate it from our own workflows.
- [ ] **C/C++ profile expansion** — Bring closer to R profile depth when someone needs it.
- [ ] **Agent development guide** — Document how to safely review and modify agent prompts.
- [ ] **CI for generated packages** — Automated checks on packages StatsClaw produces.
- [ ] **Registry submission** — CRAN / PyPI / SSC submission support via shipper.

---

## Rough Timeline

```text
Apr 8–14:   Phase 0 — onboarding basics
Apr 15–25:  Phase 1 — self-testing
Apr 25–May 15: Phase 2 — paper-to-package (exploratory)
May 15–31:  Phase 3 — interactive specification improvements
Ongoing:    Infrastructure + more working examples
```

---

## How We Think About Progress

The most useful thing we can do right now is produce more working examples — packages with enough complexity that a statistician looks at them and thinks "this saved me real time." The probit example shows the framework can build from a spec. R2PY shows it can handle a larger scope. We need more, and more varied.

Pipeline isolation — where build, test, and simulation agents can't see each other's specs — is the core architectural idea. When independent pipelines converge, that's meaningful evidence. But the idea needs more evidence behind it, not marketing in front of it.

---

## Get Involved

This roadmap is shaped by the people who use StatsClaw. Here's how to participate:

### Vote on priorities

Every roadmap item has a matching [issue in this repo](https://github.com/statsclaw/roadmap/issues). Add a 👍 to the items you care about. We use these votes to decide what to work on next — the most-upvoted items move up.

### Show what you built

If you've used StatsClaw to build or improve a package, open a PR to add it to [`SHOWCASE.md`](SHOWCASE.md). A short description and a link to the repo is all it takes. Real usage examples are the most valuable thing this project can have.

### Propose a new direction

Have an idea that isn't on the roadmap? [Open an RFC issue](https://github.com/statsclaw/roadmap/issues/new?template=rfc.yml) describing what you want and why. If the community is interested, it gets added.

### Claim a task

See something on the roadmap you'd like to work on? Comment on its issue to claim it. We'll coordinate to avoid duplicate effort. Contributions don't have to be code — profiles, documentation, test cases, and example workflows all count.

### Other ways to contribute

- **Feature requests**: [Open an issue on the main repo](https://github.com/statsclaw/statsclaw/issues/new?template=feature-request.yml)
- **Paper-to-Package requests**: [Submit a paper](https://github.com/statsclaw/statsclaw/issues/new?template=paper-to-package.yml)
- **Discussions**: [Ideas board](https://github.com/statsclaw/statsclaw/discussions/categories/ideas)
- **Code contributions**: [CONTRIBUTING.md](https://github.com/statsclaw/statsclaw/blob/main/CONTRIBUTING.md)
