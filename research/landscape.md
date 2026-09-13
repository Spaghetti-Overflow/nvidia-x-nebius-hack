# Coding-agent harness landscape

**Status:** research, not project truth

**Last checked:** 2026-09-13

This matrix compresses first-party evidence. “Bet” is an inference about the architectural emphasis, not a vendor claim. Follow the linked case file before relying on a row.

| System | Loop and context/state | Tools, execution, verification | Extension/control model | Primary bet and trade-off |
|---|---|---|---|---|
| [Claude Code](competitors/claude-code.md) | Adaptive gather → act → verify loop; session history compacts; subagents have isolated context | Built-in file/search/shell/web/code-intelligence tools; permissions and hooks gate actions | `CLAUDE.md`, skills, MCP, hooks, plugins, subagents/teams | **Inference:** integrated, model-aware product loop plus many controlled extension points. Strong UX; core internals remain vendor-owned. |
| [OpenAI Codex](competitors/openai-codex.md) | Thread/turn protocol; long tasks, compaction, steering, parallel agents/worktrees | Local OS sandbox or cloud isolated environment; approvals, network rules, tests/commands | `AGENTS.md`, skills, MCP/apps, rules; open-source CLI/app-server protocol | **Inference:** bounded computer use and supervision across local/cloud surfaces. Rich control plane increases policy/protocol complexity. |
| [DeepSeek Harness](competitors/deepseek-harness.md) | Replaceable agent driver over durable session-event log; request/tool lifecycle exposed as events | Registries and capability services; sandbox, tools, models are plugins | Cordis services, typed events, reversible effects; config-composed profiles/bundles | **Inference:** maximum recomposability with traceable state. Powerful experimentation, but abstraction/load-order/config costs and preview instability are real. |
| [OpenCode](competitors/opencode.md) | Session-oriented model loop with automatic compaction and child sessions | Built-in/custom/MCP tools; fine-grained allow/ask/deny permissions | Configured primary/subagents; JS/TS plugins and event hooks | **Inference:** provider-neutral, hackable developer client/server. Breadth and fast evolution can make stable extension contracts harder to judge. |
| [OpenHands](competitors/openhands.md) | Stateless agent steps over conversation/event state; condensers manage history | Typed tools against local, Docker, or remote workspaces; security analyzer and stuck detection | Modular SDK, skills, tools, MCP, plugins; REST/WebSocket Agent Server | **Inference:** reusable production agent SDK/runtime separation. Broad platform surface is heavier than a benchmark-focused loop. |
| [mini-SWE-agent](competitors/mini-swe-agent.md) | Very small query → execute actions → append observations loop; plain message trajectory | Usually shell/tool calls through interchangeable local/container environments | Duck-typed Agent/Model/Environment protocols plus YAML/import paths | **Inference:** capable models need little scaffolding. Readability and experimental control win; fewer built-in governance/product features. |
| [SWE-agent](competitors/swe-agent.md) | Configurable agent with history processors, parsers, hooks, and trajectories | Purpose-designed ACI/tool bundles and environment execution; task submission and limits | YAML configuration and Python extension points | **Fact:** now maintenance-only and superseded by mini-SWE-agent. Rich experimentation surface carries more complexity. |
| [Aider](competitors/aider.md) | Interactive pair-programming chat; selected files plus ranked repository map; optional architect/editor split | Model-specific edit formats; local lint/test loop; tight Git auto-commit/undo | Models, prompts, commands, config, edit/coder classes | **Inference:** optimize the human–model edit contract and repository context, not autonomous runtime orchestration. Limited isolation/orchestration compared with agent platforms. |

## Cross-cutting observations

**Facts from the case files**

- Every system closes some version of model → action → observation → next-request; differentiation is largely in what surrounds and constrains that cycle.
- State strategies differ materially: chat history, append-only events, explicit conversation state, Git commits, and immutable execution snapshots solve different recovery/audit needs.
- The strongest context strategies are selective: compaction, retrieval, repository maps, scoped instructions, or isolated subagent contexts.
- “Extensible” ranges from prompts/configuration, through registered tools/hooks, to replacing the loop and persistence service themselves.

**Opportunity hypotheses—not decisions**

- Make the relationship between an agent claim and its reproducible execution evidence legible to developers.
- Treat branching sandbox state as an evaluation/search primitive rather than merely remote shell hosting.
- Reduce the cost of changing one harness strategy while preserving the same model, task, environment, and budget.
- Improve recovery from partial actions without hiding abandoned side effects or failed trajectories.

These are prompts for [`../ideas/`](../ideas/README.md), not product proposals by themselves.
