# Coding-harness architecture patterns

**Status:** cross-system research, not a selection

**Last checked:** 2026-09-13

Evidence base: the systems in [`landscape.md`](landscape.md), particularly the explicit loops in [Claude Code](https://code.claude.com/docs/en/how-claude-code-works), [mini-SWE-agent](https://mini-swe-agent.com/v2/advanced/control_flow/), [OpenHands](https://docs.openhands.dev/sdk/arch/agent), and [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md).

## Responsibilities a useful harness cannot avoid

Even when implemented in one function, a harness must own these invariants:

1. **Admission:** which user/context input belongs to the next model request.
2. **Action protocol:** how model output becomes a validated action and observation.
3. **Authority:** what may execute, in which environment, with which permissions.
4. **Ordering:** how concurrent calls, steering, retries, cancellation, and termination settle.
5. **State truth:** what record can reconstruct model-visible history and side effects.
6. **Budgets:** when calls, time, tokens, cost, or failures stop the run.
7. **Evidence:** how completion and correctness are distinguished from confident text.

Removing a “core” package does not remove these responsibilities; it distributes them across plugins and their contracts.

## Architecture styles

| Style | Shape | Advantages | Costs/failure modes | Best evidence for use |
|---|---|---|---|---|
| Integrated/monolithic harness | Loop calls concrete context, tools, runtime, and state components | Fast to build; easy local reasoning; few indirections | Harder controlled swaps; policy can scatter; tests couple to internals | One narrow workflow and stable requirements |
| Stable core + adapters | Core owns lifecycle/invariants; interfaces vary providers | Clear ownership; good test seams; moderate complexity | “Core” can accrete features; adapters may leak provider semantics | Several backends must preserve the same lifecycle |
| Microkernel/capabilities | Small lifecycle/kernel; capabilities register via services/registries | Independent composition; local extensions; replaceable providers | Dependency/lifecycle semantics become a second system | Runtime experimentation is itself user value |
| Highly plugin-oriented | Loop, state, tools, UI, and providers are configured plugins | Maximum recombination; profiles become reproducible experiments | Contract/version churn, startup diagnosis, abstraction tax, large test matrix | Users truly replace whole strategies, not just add tools |

DeepSeek Harness is strong evidence that even “everything is a plugin” retains invariants in a kernel and shared vocabulary: Cordis owns dependency-aware mounting and reversible effects; shared types/services define interaction; durable session events constrain model-visible state. See the [case study](competitors/deepseek-harness.md).

## Replaceability by capability

| Capability | Replacement value | Contract pressure |
|---|---|---|
| Model backend | High: pricing, latency, modality, provider availability | Normalize without erasing streaming, caching, reasoning, and tool-call semantics |
| Tool registry/ACI | High: user/domain differentiation and experiments | Schema versioning, permissions, bounded outputs, idempotency |
| Sandbox backend | High when local/cloud/branching environments matter | Filesystem identity, process lifecycle, network, secrets, cancellation, artifacts |
| Verifier | High because correctness is task-specific | Determinism, trusted execution, attribution, pass/fail versus graded scores |
| Context strategy | High for long or large-repository tasks | Provenance, cache boundaries, compaction loss, token accounting |
| Persistence | Moderate/high for resume, audit, forks, and scale | Atomic ordering, migrations, single-writer rules, partial failures |
| Agent loop/search policy | Valuable mainly for research or distinct workflows | Broadest contract: it touches nearly every invariant and multiplies test cases |

**Inference:** models, sandbox providers, tool sets, and verifiers usually earn interfaces earlier than the whole loop. A replaceable loop is credible only if controlled experiments or product use cases require different lifecycle policies.

## Communication mechanisms

| Mechanism | Use it for | Avoid when |
|---|---|---|
| Direct calls | Mandatory ordered control flow with one owner | Many optional observers or hot replacement |
| Interfaces/services | One capability with alternative providers | Only one trivial implementation exists |
| Registry | Many independently contributed tools/models/verifiers | Global mutable ordering would be ambiguous |
| Events | Observation or explicit interception at lifecycle boundaries | A return value/transaction must be guaranteed without a clear dispatch contract |
| Durable event log | Audit, replay, resume, projections, fork lineage | Side effects cannot be correlated or schema migrations are ignored |

A practical hybrid is common: direct lifecycle calls, service interfaces at valuable seams, registries for N-way contributions, transient events for observation/interception, and a durable log for facts. The owner of ordering and error semantics must remain explicit.

## Cost of abstraction

- More interfaces increase integration tests, versioning, diagnostics, configuration, and cognitive load.
- A lowest-common-denominator API can hide provider advantages; a leaky API defeats replacement.
- Runtime unload/reload requires ownership and cleanup semantics, not merely dependency injection.
- Every extension point enlarges the permission and supply-chain surface.
- A stable event vocabulary can be more constraining than concrete code because persistence makes it a compatibility contract.

## Open questions for our team

- Which selected user problem benefits from changing harness components at runtime or between runs?
- What is the single source of truth for model-visible history and execution side effects?
- Which lifecycle invariants must remain fixed across strategies?
- Do we need append-only replay, Git state, sandbox snapshots, or a deliberate combination?
- Are branch/search policies a product behavior, an evaluation technique, or unnecessary complexity?
- Which capability swaps must be demonstrated with the same model/task/environment/budget?
- How will a failed, cancelled, or timed-out action be represented without implying it never happened?
- What extension surface can a five-person team secure, document, test, and demo convincingly?
