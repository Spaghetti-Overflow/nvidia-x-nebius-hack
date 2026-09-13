# mini-SWE-agent

**Status:** competitor research

**Last checked:** 2026-09-13

**Version focus:** v2

## What it is

mini-SWE-agent is a deliberately small software-engineering agent from the SWE-agent team. It targets issue solving, benchmarks, and terminal work while keeping the core agent readable in roughly a hundred lines.

## Architecture evidence

- **Loop:** initialize messages; repeatedly query the model, execute every returned action through the environment, format observations, append them, and stop on an exit/flow-control condition.
- **Seams:** Agent, Model, and Environment are duck-typed protocols. Run scripts choose one of each. YAML accepts alternative classes or import paths.
- **Responsibility placement:** v2 models parse actions and format observation messages; the agent coordinates and owns call/cost limits; environments execute actions.
- **Execution:** interchangeable local, Docker, Singularity/Apptainer, Bubblewrap, SWE-ReX, Modal, and ConTree environments. Local execution has no isolation.
- **State/observability:** message history is the working context and runs can emit full JSON trajectories; a trajectory browser supports inspection.
- **Verification:** tests are normally model-invoked shell work or benchmark evaluators rather than a large built-in verifier subsystem.

## Strengths

- Minimal control flow makes causal experiments and failure diagnosis easier.
- Small protocols make model/environment swaps cheap without a plugin framework.
- Strong fit for reproducible batch evaluation and training scaffolds.

## Trade-offs

- Product concerns such as rich approval UX, durable multi-user sessions, policy governance, and multi-agent orchestration are intentionally sparse.
- Plain-history designs can need custom treatment for very long tasks or rich state provenance.
- Simplicity moves some responsibility into prompts, models, run scripts, and external evaluation infrastructure.

## Questions for us

- What can remain a simple run-script composition rather than a runtime plugin system?
- Which additional capability demonstrably improves the same model/task/environment baseline?
- Does our eventual user need governance and persistence beyond a benchmark runner?

## First-party sources

- [Repository and motivation](https://github.com/SWE-agent/mini-swe-agent)
- [v2 control flow](https://mini-swe-agent.com/v2/advanced/control_flow/)
- [Environment backends](https://mini-swe-agent.com/latest/advanced/environments/)
- [v2 architecture changes](https://mini-swe-agent.com/latest/advanced/v2_migration/)
- [Configuration](https://mini-swe-agent.com/latest/advanced/yaml_configuration/)
