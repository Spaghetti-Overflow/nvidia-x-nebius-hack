# OpenHands

**Status:** competitor research

**Last checked:** 2026-09-13

## What it is

OpenHands V1 is a multi-repository developer-agent platform. The Software Agent SDK owns agents, tools, conversations, workspaces, events, and Agent Server; Agent Canvas is the UI; a separate automation service owns schedules/webhooks and dispatch.

## Architecture evidence

- **Loop:** a stateless `Agent.step()` reasons over a conversation view, executes/validates tool calls, appends observations, and continues until a final response or limit.
- **State:** `Conversation` owns lifecycle and `ConversationState`; an immutable append-only `EventLog` records history. The Agent Server persists metadata and JSONL events for resume.
- **Context:** condensers reduce history near context limits; skills and `AgentContext` contribute prompts/metadata.
- **Tools/security:** typed tools produce actions/observations; a security analyzer can evaluate actions. Stuck detection and iteration/cost bounds are explicit runtime services.
- **Execution:** workspaces abstract local versus remote execution. V1 sandbox providers include Docker (recommended), unsafe direct process, and remote sandboxes. Agent Server exposes execution through REST/WebSocket.
- **Extensibility:** custom tools, agents, skills, MCP, plugins, workspace providers, condensers, and security analyzers are modular SDK seams.

## Strengths

- Clear separation of stateless reasoning, durable conversation state, and execution workspace.
- Embeddable SDK plus remote server and UI/automation boundaries.
- Typed event/tool model supports inspection and alternate workspace backends.

## Trade-offs and unknowns

- It is a broad platform with several repositories and deployment services; setup and version alignment are heavier than a small research harness.
- Current V1 differs materially from legacy V0 runtime/controller architecture; old diagrams can mislead.
- Local process mode is explicitly unsafe; Docker isolation strength depends on deployment configuration.

## Questions for us

- Would a stateless agent over an explicit conversation/event state simplify replay and tests?
- Which component boundaries are driven by real multi-client deployment needs?
- Can we avoid importing platform breadth before the user workflow requires it?

## First-party sources

- [Software Agent SDK repository](https://github.com/OpenHands/software-agent-sdk)
- [Agent architecture](https://docs.openhands.dev/sdk/arch/agent)
- [Conversation architecture](https://docs.openhands.dev/sdk/arch/conversation)
- [V1 sandbox providers](https://docs.openhands.dev/openhands/usage/sandboxes/overview)
- [Current repository boundaries](https://github.com/OpenHands/OpenHands)
