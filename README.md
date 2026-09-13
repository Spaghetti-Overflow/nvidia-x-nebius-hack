<p align="center">
  <img
    src=".assets/images/hackathon-banner.png"
    alt="Nebius x NVIDIA Global AI Hackathon — Build the next frontier of AI on open infrastructure"
    width="100%"
  />
</p>

<h1 align="center">NVIDIA × Nebius Hack 2026</h1>

<p align="center">
  An agent-first discovery and delivery workspace for the<br />
  <strong>Coding and Agentic Engineering</strong> track.
</p>

<p align="center">
  <a href="https://nebiusglobalaihackathon.devpost.com/">Hackathon</a>
  ·
  <a href="docs/hackathon.md">Requirements</a>
  ·
  <a href="research/README.md">Research</a>
  ·
  <a href="ideas/README.md">Ideas</a>
  ·
  <a href="AGENTS.md">Agent guide</a>
</p>

> [!IMPORTANT]
> This project is in **discovery**. The user problem, product thesis, stack, and architecture have not been selected. Coding agents and harnesses are the exploration area—not a predetermined product.

## What this repository is

This repository is the team's shared operating system for moving from evidence to a focused hackathon product. It keeps official constraints, external research, product hypotheses, accepted decisions, implementation, and evaluation artifacts separate so that humans and coding agents can collaborate without turning assumptions into facts.

The current investigation covers coding agents, harnesses, context engineering, agent runtimes, sandboxed execution, verification, state management, extensibility, and developer tooling.

| Project signal | Current state |
|---|---|
| Track | Coding and Agentic Engineering |
| Phase | Discovery and problem selection |
| Product | Undecided |
| Architecture and stack | Undecided |
| Implementation | Intentionally not started |
| Submission deadline | October 30, 2026 at 10:00 AM PDT |

## Repository map

| Path | Source of truth for |
|---|---|
| [`AGENTS.md`](AGENTS.md) | Repository-wide routing and collaboration rules |
| [`docs/hackathon.md`](docs/hackathon.md) | Official requirements, dates, judging criteria, and submission checklist |
| [`docs/product.md`](docs/product.md) | The accepted product definition once the team chooses one |
| [`docs/architecture.md`](docs/architecture.md) | Accepted architecture and its still-open questions |
| [`docs/evaluation.md`](docs/evaluation.md) | Evaluation policy, comparison discipline, and evidence requirements |
| [`docs/decisions/`](docs/decisions/README.md) | Architecture Decision Records for material choices |
| [`research/`](research/README.md) | Sourced external evidence and technical analysis |
| [`ideas/`](ideas/README.md) | Candidate problems and product hypotheses |
| [`app/`](app/README.md) | Future implementation, tests, scripts, and evaluations |

## Research baseline

The initial research package is ready to support product discovery:

- [`landscape.md`](research/landscape.md) compares Claude Code, Codex, DeepSeek Harness, OpenCode, OpenHands, mini-SWE-agent, SWE-agent, and Aider.
- [`deepseek-harness.md`](research/competitors/deepseek-harness.md) is the deeper architecture case study.
- [`architecture-patterns.md`](research/architecture-patterns.md) extracts cross-system harness patterns and their trade-offs.
- [`sandboxes.md`](research/sandboxes.md) records verified Nebius Token Factory Sandboxes capabilities and open questions.
- [`harness-primer.md`](docs/harness-primer.md) provides a vendor-neutral shared vocabulary.

Research is evidence, not a decision. Any material product or architecture choice must be accepted explicitly and recorded in the canonical docs or an ADR.

## How we work

1. Read [`AGENTS.md`](AGENTS.md) before making changes.
2. Check [`docs/hackathon.md`](docs/hackathon.md) before proposing anything that affects eligibility or submission.
3. Add sourced findings to `research/`; add unvalidated product hypotheses to `ideas/`.
4. Promote a direction into `docs/product.md` only after the team accepts it.
5. Record material technical choices in [`docs/decisions/`](docs/decisions/README.md) before implementation depends on them.
6. Keep empirical runs under `app/evals/` and commit only curated, reproducible reports.

The working order is:

```text
problem → user → insight → solution → architecture → technology → evaluation
```

## Hackathon guardrails

The final submission must include working software that uses at least one NVIDIA open-source model and makes a runtime inference call through Token Factory or runs on eligible Nebius AI Cloud compute. It also needs a public source repository, setup instructions, a license, a hosted demo or test build, and an English demo video under three minutes.

See the team's [operational requirements digest](docs/hackathon.md) and the [official rules](https://nebiusglobalaihackathon.devpost.com/rules) before relying on this summary.

## License

No license has been selected yet. Choosing and adding one is a required pre-submission decision.
