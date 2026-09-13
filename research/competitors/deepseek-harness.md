# DeepSeek Harness

**Status:** required architecture case study; research only

**Last checked:** 2026-09-13

**Maturity:** developer preview; official notice says core plugins and APIs will evolve

## What it fundamentally is

DeepSeek Harness is an open-source agent harness and distribution built on the vendored Cordis plugin framework. Its stated design is “everything is a plugin”: models, tools, skills, sessions, sandboxes, storage, loops, scheduling, and UI are selected and composed through configuration.

This does **not** mean there is no core mechanism. The distinction is:

- Cordis is the kernel that owns plugin contexts, dependency-aware lifecycle, services, typed events, and reversible effects.
- Harness packages provide shared contracts and default implementations.
- Profiles/bundles provide runnable compositions.

## What is core in practice

The official `packages/core` group is a default API spine, not an unreplaceable kernel:

| Package/capability | Responsibility | Replaceability |
|---|---|---|
| `session` | Append-only `SessionEvent` log and in-memory store | Service/provider composition can change; event vocabulary remains a shared contract |
| `system-prompt` | Ordered prompt sections, variables, tool schemas | Contributions are registered/scoped |
| `tools` | Scoped registry and guarded execution pipeline | Tools/providers/interceptors are replaceable/extensions |
| `agent` | Public `Agent` handle, registry, inbox, lifecycle event contract | Stable seam consumed by extensions |
| `agent-loop` | Concrete default driver implementing `Agent` | Explicitly replaceable; extensions depend on `agent`, not the driver |
| `scope` | Per-agent scoped-registration primitive | Dependency-free library below services |
| `llm` | Message/stream vocabulary and adapter registry | Provider adapters are replaceable |

**Inference:** the minimum operational core is not “nothing”; it is Cordis lifecycle plus whichever service contracts a selected composition makes mutually dependent. The default product spine is broader than the kernel.

## Composition, lifecycle, and dependencies

- A profile names ordered bundles and local patches. Bundles contribute Cordis configuration rows. Layer order is bundles → profile patch → home patch → CLI overlay.
- Patches address stable row IDs and replace a row's whole config or insert rows; they are not deep merges.
- Plugins declare required services through `inject`. They wait until providers exist, unload when a required service disappears, and may reload when it returns.
- A contribution registered through Cordis is an owned effect. Unmounting its plugin unwinds registrations; external resources must register a disposer with `ctx.effect()`.
- Services (`ctx.tools`, `ctx.llm`, `ctx.agents`, and others) provide direct capability interfaces. Typed broadcast/waterfall events provide observation and interception. Registries accept N-way contributions.
- Service isolation allows separate plugin groups to receive different providers under the same service key.

This puts lifecycle in Cordis and domain ordering in the agent/session/tool implementations—not in arbitrary plugins.

## Agent loop and action lifecycle

A turn contains zero or more steps; a step is one model request plus resulting tool calls. The default driver:

1. Claims input from one inbox and lets `agent/pre-step` admit, rewrite, or reject it.
2. Assembles system prompt and tool schemas.
3. Resolves the prepared model route before committing model-visible input.
4. Appends durable request/user events and freezes request history derived from the log.
5. Streams the model result, durably settling a complete assistant message or failed attempt.
6. Runs tool calls through `tools/pre-execute` → `tools/execute` → `tools/post-execute`, then records results.
7. Continues if tools or new input require another request; otherwise settles the turn.

Waterfall events can wrap/intercept request and tool phases. Cancellation has explicit settlement rules. The loop can be swapped because consumers target the `Agent` contract/factory, but any alternative must preserve the contracts expected by its selected plugins.

## Representation of major capabilities

- **Models:** adapters register with the LLM service; the request route is prepared before model-visible inputs commit.
- **Tools:** scoped registry entries contribute schema/prompt presentation and execute through a guarded event pipeline.
- **Sandboxes:** per-session policy resolves a mode/root; consumers request confined process arguments from a provider. A confined policy must fail closed when no backend is available.
- **Filesystem/shell:** providers share an execution world so swapping to a remote environment can move related capabilities together.
- **State:** append-only session events are the source of model history; transient streaming events serve live UI without becoming durable history prematurely.
- **Context:** ordered prompt sections, injected context, tools, session-log projection, and compaction are separate seams.
- **Subagents:** a provider interface supports in-process, forked, ACP, Codex, Claude Code, or SDK-backed implementations; optional tools expose delegation/control.

## Persistence and history

- `SessionPersistence` is an abstract handle-based seam with create/open/stat/list/export semantics and read/append/flush/close per-session handles.
- JSONL and SQLite providers are documented. The write handle enforces single-writer ownership; `flush` is the durability barrier.
- Resume repairs an interrupted turn by appending explicit missing error/end events under write ownership rather than erasing durable partial work.
- Fork/resume/transcript/telemetry derive from settled session events. The governing invariant is: **model-visible means logged**.
- Stored formats have versioning/migration rules. This is a reminder that a “replaceable” persistence backend still implements strict logical invariants.

## Architectural invariants that remain

1. Plugin ownership and cleanup must be reversible.
2. Required services govern activation and disposal.
3. Model-visible content must be reconstructable from the durable session log.
4. Request/tool/turn events have defined ordering and dispatch semantics.
5. Session persistence respects contiguous ordering, ownership, flush, and format compatibility.
6. Sandboxed execution fails closed when confinement is required.
7. Shared public types and service keys constrain independently replaceable implementations.

## Strengths

- Unusually broad, inspectable replaceability, including the agent driver and persistence provider.
- Configured compositions can support controlled harness experiments without source forks.
- Strong lifecycle teardown and durable trajectory model make dynamic composition less ad hoc.

## Trade-offs and risks

- The framework, service graph, config layering, event taxonomy, generated catalogs, and package granularity impose a steep cognitive/tooling cost.
- Whole-row patch replacement and pending dependencies can make configuration mistakes non-local.
- Replacing the loop does not remove compatibility obligations; it moves them into contracts and tests.
- Dynamic/out-of-tree plugins enlarge supply-chain, permission, versioning, and state-migration risks.
- Developer preview status makes current APIs a poor fixed foundation without pinning and validation.

## Lessons/questions—not adoption decisions

- A microkernel needs explicit ownership, disposal, and dependency semantics; an interface registry alone is insufficient.
- “Everything replaceable” is useful only when users or experiments actually replace it.
- Durable event truth can unify replay, observability, context, and recovery, but becomes a demanding schema contract.
- Which two or three seams would produce user value for our eventual problem? Which would only demonstrate architecture?
- Can the same experimental value be achieved with a stable core and adapters at much lower cost?

## First-party sources

- [Developer preview overview](https://www.deepseek.com/harness/en/)
- [Architecture](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md)
- [Core subsystem](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/core.md)
- [Core package map](https://github.com/deepseek-ai/deepseek-harness/blob/master/packages/core/README.md)
- [Cordis primer/tutorial](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-tutorial/index.md)
- [Services and dependencies](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/develop/framework/service.md)
- [Lifecycle and reversible effects](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-tutorial/02-lifecycle-and-effects.md)
- [Session persistence](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/persistence.md)
- [Sandbox subsystem](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/sandbox.md)
- [Subsystem index](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/subsystems/README.md)
