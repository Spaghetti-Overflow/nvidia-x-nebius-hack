# Coding-agent harness primer

**Status:** shared, vendor-neutral mental model
**Last reviewed:** 2026-09-13

A coding-agent harness is the system around a model that turns model outputs into controlled, stateful work in a software environment. It is infrastructure, not inherently a product or differentiator.

## Generic loop

```text
task + policy + selected context
  → model request
  → proposed message or action(s)
  → authorize and execute actions
  → capture observations and state changes
  → verify progress / decide whether to continue
  → repeat, recover, or finish
```

The loop is rarely a clean linear cycle: tools can run concurrently, users can steer mid-turn, calls can fail, context may compact, and durable state must remain coherent.

## Responsibilities

| Capability | Responsibility | Example implementation choices |
|---|---|---|
| Model interaction | Normalize requests, streaming, retries, limits, and provider quirks | Direct SDK, gateway, adapter registry |
| Agent policy/loop | Decide request/action/termination sequence | Fixed ReAct loop, planner/executor, replaceable driver |
| Context management | Select, order, cache, compact, and provenance-track model-visible information | Full transcript, summaries, repo map, retrieval |
| Tool/ACI layer | Present actions, validate inputs, return bounded observations | Function calls, shell-only interface, edit protocol |
| Execution | Run commands and manipulate files | Local subprocess, container API, remote worker |
| Sandbox/runtime | Enforce isolation, resources, network, and lifetime | OS sandbox, container, microVM |
| Repository state | Track working tree, checkpoints, diffs, branches, and recovery | Git, snapshots, copy-on-write images |
| Verification | Convert outputs into evidence about correctness | Tests, linters, type checks, task-specific judges |
| Persistence | Preserve sessions, events, artifacts, and resumability | Append-only log, database, JSONL |
| Permissions/security | Gate capabilities and sensitive boundaries | Allowlists, approval workflow, policy engine |
| Observability | Explain model inputs, actions, failures, cost, and outcomes | Event log, traces, metrics, trajectory viewer |
| Orchestration | Coordinate subtasks, agents, branches, budgets, and merging | Parent/child sessions, task graph, beam search |

## Capability is not implementation

An **execution environment** is a capability; a particular sandbox provider is one implementation. **Persistence** is a capability; SQLite or JSONL are implementations. **Context reduction** is a capability; summarization and graph-ranked repository maps are different implementations.

This distinction prevents two errors: treating a vendor choice as a requirement, and adding abstraction before evidence shows replaceability is valuable. Architecture research belongs in [`../research/architecture-patterns.md`](../research/architecture-patterns.md); accepted choices belong in [`architecture.md`](architecture.md).
