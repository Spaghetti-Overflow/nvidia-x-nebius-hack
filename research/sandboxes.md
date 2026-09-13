# Nebius Token Factory Sandboxes / ConTree

**Status:** external research; no architecture choice

**Last checked:** 2026-09-13

Nebius documents Token Factory Sandboxes as the productized ConTree service. It is currently **Beta**. The authoritative starting point is the [Token Factory Sandboxes overview](https://docs.tokenfactory.nebius.com/sandboxes/overview); the [ConTree site](https://contree.dev/) provides additional first-party operational detail.

## Verified capabilities

| Capability | Verified behavior | Source |
|---|---|---|
| Execution/isolation | Commands run in a microVM with VM-level isolation; each execution returns stdout, stderr, exit code, metrics, and optionally new state | [Overview](https://docs.tokenfactory.nebius.com/sandboxes/overview), [ConTree concepts](https://contree.dev/#concepts) |
| Base environments | Start from preloaded state, a prior checkpoint, or imported OCI images | [Overview](https://docs.tokenfactory.nebius.com/sandboxes/overview) |
| Filesystem state | A non-disposable execution produces an immutable filesystem image/checkpoint; process memory, running services, and network state are not preserved | [ConTree FAQ](https://contree.dev/#faq) |
| Branch/rollback | Multiple executions can start from one checkpoint; returning to an earlier image is rollback by reference rather than replay | [Overview](https://docs.tokenfactory.nebius.com/sandboxes/overview), [SDK branching guide](https://docs.tokenfactory.nebius.com/sandboxes/sdk/python_sdk/branching) |
| Parallel/async work | Operations are asynchronous, pollable, cancellable, and may be launched in parallel | [Overview](https://docs.tokenfactory.nebius.com/sandboxes/overview) |
| Disposable runs | A run may return output without saving a new image, useful for tests/linters | [ConTree concepts](https://contree.dev/#concepts) |
| File workflows | SDK/API support upload/sync, list/read without a VM, and artifact download; MCP exposes these to compatible agents | [MCP docs](https://docs.tokenfactory.nebius.com/sandboxes/mcp), [SDK docs](https://docs.tokenfactory.nebius.com/sandboxes/sdk) |
| Repository/eval starting points | More than 7,000 SWE environments are documented as preloaded, including SWE-bench Verified and SWE-rebench datasets | [Sandboxes for SWE agents](https://docs.tokenfactory.nebius.com/sandboxes/swe-agents) |
| Interfaces | Python sync/async SDK, CLI, REST API, and MCP server | [Overview resources](https://docs.tokenfactory.nebius.com/sandboxes/overview#resources) |
| Metrics | CPU time, memory, and I/O metrics are tracked per execution | [Overview](https://docs.tokenfactory.nebius.com/sandboxes/overview) |
| Limits/maturity | Beta; 50 simultaneous operations; untagged, unreferenced checkpoint images may be deleted after 180 days | [Beta limitations](https://docs.tokenfactory.nebius.com/sandboxes/overview#beta-limitations) |
| Latency | ConTree states cached-rootfs microVM startup is about 0.4–2 seconds; treat as vendor-reported and measure for our region/workload | [ConTree FAQ](https://contree.dev/#faq) |

## Important boundaries and unknowns

- **Network policy:** first-party pages state no inbound access; some MCP copy says “network” is available. Default outbound access, allowlisting, and per-run egress controls are not specified clearly enough for an architecture assumption. Verify in the actual beta account.
- **Resource controls:** metrics and timeouts are described, but public docs reviewed here do not establish all configurable CPU, memory, disk, output, runtime, or quota ranges.
- **Secrets:** guidance says pass secrets through environment variables, but secret lifetime, masking, and snapshot exclusion need hands-on verification before using credentials in agent-written code.
- **Merge semantics:** branching and choosing a resulting image are verified. Automatic source-level merging of several branch filesystems is not; assume selection/export must be orchestrated.
- **Durability/SLA:** checkpoint retention behavior is documented for beta, but availability, regional placement, backup, and recovery guarantees were not verified.
- **API maturity:** names and contracts can change while the product is in Beta. Pin SDK versions and record API/service versions in experiments.

## Possible harness opportunities

These are hypotheses, not product or architecture decisions.

- Use identical checkpoint ancestry to compare two harness strategies without environment drift.
- Speculatively run candidate fixes from one known-good state and evaluate them in parallel.
- Preserve failed branch artifacts for diagnosis while advancing only a verified branch.
- Separate state-changing build/setup actions from disposable verification runs to reduce snapshot noise and storage.
- Join sandbox lineage, model/tool trajectory, and verifier results into one reproducible experiment record.

Before adoption, run a spike covering authentication, repository sync, dependency install, command cancellation, test output limits, checkpoint branching, concurrent quota behavior, artifact retrieval, egress, secret leakage, and measured cold/warm latency.
