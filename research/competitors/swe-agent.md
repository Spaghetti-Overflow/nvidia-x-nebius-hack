# SWE-agent

**Status:** competitor research

**Last checked:** 2026-09-13

**Current status:** maintenance-only; maintainers recommend mini-SWE-agent

## What it is

SWE-agent is the Princeton/Stanford research system that introduced deliberate agent-computer interfaces (ACIs) for autonomous software-engineering tasks. It remains useful as architecture history and a configurable experimental harness.

## Architecture evidence

- **Loop/state:** an Agent holds message history, model statistics, environment state, and a saved trajectory; hooks can observe its lifecycle.
- **ACI/tools:** configurable tool bundles, command documentation, action parsers, execution timeouts, state commands, and submission commands shape the model-computer contract.
- **Context:** history processors transform model-visible history and support concerns such as cache breakpoints; prompt/templates and parser choices are YAML configured.
- **Execution:** tools operate through a selected SWE-ReX environment; configuration controls environment variables, reset/install behavior, and action time limits.
- **Verification:** benchmark tasks use explicit submission/evaluation; during a run the model can invoke test tools, but a successful submission is not itself proof.
- **Extensibility:** Python classes, tools, parsers, hooks, history processors, and one main YAML configuration expose a broad research surface.

## Strengths

- Made the ACI a first-class experimental variable rather than treating shell syntax as incidental.
- Detailed trajectories/configuration support reproducible research.
- Rich history/tool controls enable targeted ablations.

## Trade-offs

- Maintainers report mini-SWE-agent reaches similar performance with much less machinery; most active development moved there.
- Many interacting configuration points widen the experimental and failure surface.
- Research benchmark defaults do not automatically form a safe, polished developer product.

## Questions for us

- Is a specialized ACI needed for the selected user/model, and how would we prove it?
- Which history transformation improves results without changing other variables?
- What did model capability growth make unnecessary, and what remains structurally important?

## First-party sources

- [Current documentation and maintenance notice](https://swe-agent.com/latest/)
- [Agent reference](https://swe-agent.com/latest/reference/agent/)
- [Tool configuration](https://swe-agent.com/latest/reference/tools_config/)
- [SWE-agent paper](https://arxiv.org/abs/2405.15793)
