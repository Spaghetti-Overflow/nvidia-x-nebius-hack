# Repository constitution

This is an agent-first discovery and delivery workspace for a five-person Nebius x NVIDIA Global AI Hackathon 2026 team. The final product, stack, and architecture are **undecided**. Coding and Agentic Engineering is the current exploration area, not a predetermined solution.

## Route by task

| Need | Canonical location |
|---|---|
| Hackathon requirements | [`docs/hackathon.md`](docs/hackathon.md) |
| Accepted product definition | [`docs/product.md`](docs/product.md) |
| Generic harness concepts | [`docs/harness-primer.md`](docs/harness-primer.md) |
| Accepted architecture | [`docs/architecture.md`](docs/architecture.md) |
| Evaluation policy | [`docs/evaluation.md`](docs/evaluation.md) |
| ChatGPT idea validator | [`docs/validate-idea-with-chatgpt.md`](docs/validate-idea-with-chatgpt.md) |
| ChatGPT idea-research workflow | [`docs/research-with-chatgpt.md`](docs/research-with-chatgpt.md) |
| Material accepted decisions | [`docs/decisions/`](docs/decisions/README.md) |
| External technical evidence | [`research/`](research/README.md) |
| Ecosystem comparison | [`research/landscape.md`](research/landscape.md) |
| Competitor evidence | [`research/competitors/`](research/competitors/) |
| Cross-system architecture patterns | [`research/architecture-patterns.md`](research/architecture-patterns.md) |
| Nebius sandbox evidence | [`research/sandboxes.md`](research/sandboxes.md) |
| Product hypotheses | [`ideas/`](ideas/README.md) |
| Implementation | [`app/`](app/README.md) |
| Empirical runs and reports | [`app/evals/`](app/evals/README.md) |

Load only the files required for the current task. Subtree instructions in `ideas/AGENTS.md` and `app/AGENTS.md` add local rules.

## Operating rules

- Before adding information or a file, search the repository for existing coverage. Update the canonical source and link to it; create new content only when it has a distinct purpose that no existing file serves.
- One concept has one canonical home. Update it and link to it; do not copy substantial content.
- Keep `docs/` to accepted facts, constraints, and explicit decisions. Never silently promote research or an idea into project truth.
- Label uncertainty. Distinguish sourced fact, inference, hypothesis, decision, and unknown.
- Verify current ecosystem claims with first-party sources; record the source and verification date.
- Do not present unresolved product, stack, or architecture choices as settled.
- Record a material project or architecture choice as an ADR before relying on it broadly. Trivial implementation choices do not need ADRs.
- Generated outputs belong under runtime/evaluation artifact paths, not in canonical knowledge. Commit only curated evaluation reports.
- Technology is a building block, not the idea. Work in the order: problem → user → insight → solution → architecture → technology.
- Never commit secrets. Preserve user changes and keep changes small, testable, and easy to review.
