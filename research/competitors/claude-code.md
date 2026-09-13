# Claude Code

**Status:** competitor research

**Last checked:** 2026-09-13

## What it is

Claude Code is Anthropic's coding-agent harness across terminal, IDE, desktop, web, and cloud surfaces. Anthropic describes its loop as gather context → take action → verify, repeated and steerable by the user.

## Architecture evidence

- **Loop:** the model receives system instructions, conversation history, and tool definitions; tool results become the next observations. The embedded Agent SDK exposes the same autonomous loop and lifecycle hooks.
- **Context/state:** project/user `CLAUDE.md` files provide persistent instructions; skills load reusable context/workflows; long sessions compact automatically. Subagents run separate contexts and return results to the parent.
- **Tools/execution:** built-ins cover files, search, shell, web, and optional code intelligence. Execution may be local or in Anthropic-managed cloud VMs depending on surface.
- **Verification:** verification is an explicit phase but remains agent-directed unless hooks, tests, or external policy make it deterministic.
- **Permissions/security:** permission modes control tool use; sandboxing can enforce filesystem/network boundaries. `PreToolUse` hooks can block or rewrite proposed actions.
- **Extensibility:** scoped instructions, skills, MCP servers, hooks, custom subagents, agent teams, and plugins attach at different layers. Hooks expose lifecycle interception without replacing the core loop.
- **Observability:** tool calls/results and session events are visible; hooks receive session and lifecycle metadata. Public docs do not establish a complete durable internal event schema.

## Strengths

- Cohesive loop and developer UX with clear human steering.
- Several extension mechanisms matched to distinct needs rather than one universal plugin abstraction.
- Strong permission/hook surface for deterministic controls around probabilistic behavior.

## Trade-offs and unknowns

- Core product implementation and many internal invariants are not public; architecture claims must stay at documented behavior/API level.
- Multiple extension mechanisms increase the choice and security surface.
- Subagent isolation reduces parent context pressure but requires good task boundaries and result synthesis.

## Questions for us

- Which controls must be deterministic hooks rather than instructions the model may ignore?
- Can scoped, progressively loaded knowledge outperform a large always-on prompt for our chosen workflow?
- What evidence should cross a child/parent boundary, and what state must remain isolated?

## First-party sources

- [How Claude Code works](https://code.claude.com/docs/en/how-claude-code-works)
- [Extend Claude Code](https://code.claude.com/docs/en/features-overview)
- [Agent SDK loop](https://code.claude.com/docs/en/agent-sdk/agent-loop)
- [Permissions](https://code.claude.com/docs/en/agent-sdk/permissions)
- [Hooks](https://code.claude.com/docs/en/agent-sdk/hooks)
