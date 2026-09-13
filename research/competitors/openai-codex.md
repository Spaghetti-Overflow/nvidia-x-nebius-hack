# OpenAI Codex

**Status:** competitor research

**Last checked:** 2026-09-13

## What it is

Codex is OpenAI's coding-agent system spanning an open-source local CLI/core, IDE and desktop clients, cloud execution, and programmatic protocols. The same broad harness concerns—context, tools, execution, approval, and supervision—appear across these surfaces, but deployment details differ.

## Architecture evidence

- **Lifecycle/state:** the app-server exposes threads containing turns and typed items, streaming notifications, steering, interruption, and resume. Long contexts can compact; the exact policy is model/config dependent.
- **Context:** repository `AGENTS.md` instructions are discovered by scope; skills add progressively disclosed workflows. Thread history and configuration can move between supported clients.
- **Tools:** shell, patch/file operations, web, MCP/apps, and other tools are exposed under a common turn stream. Tool schemas and approvals are surfaced as protocol items.
- **Execution:** local commands run under OS-level sandbox policies; cloud tasks receive isolated environments. Desktop worktrees isolate parallel repository changes.
- **Permissions/security:** sandbox mode and approval policy are separate. Filesystem/network boundaries, command approvals, managed policies, and telemetry form a layered control plane.
- **Verification:** the model is trained/instructed to run tests and inspect changes; clients expose diffs for human review. Tests are evidence only when task-specific and recorded.
- **Extensibility:** `AGENTS.md`, skills, MCP, apps/connectors, rules, and client/app-server integration. The public code makes protocol and execution layers inspectable; it does not imply every hosted component is open source.

## Strengths

- Explicit separation between technical sandbox bounds and human/managed approval policy.
- Strong multi-surface thread/turn protocol and diff-centered supervision.
- Local and cloud execution options plus worktree-based parallelism.

## Trade-offs and unknowns

- Product surfaces evolve quickly and do not all share identical capabilities or isolation.
- A rich approval/protocol model creates substantial state-machine and client compatibility work.
- Hosted orchestration and model-side strategies are not fully inferable from the open-source CLI.

## Questions for us

- Do we need a stable event protocol for more than one client, or would that be premature?
- Which risks require enforced sandbox boundaries versus approval UX?
- Is worktree isolation sufficient, or does the problem require full environment snapshots/branching?

## First-party sources

- [Open-source Codex repository](https://github.com/openai/codex)
- [App-server protocol](https://github.com/openai/codex/blob/main/codex-rs/app-server/README.md)
- [Repository instructions (`AGENTS.md`)](https://developers.openai.com/codex/guides/agents-md)
- [Configuration reference](https://developers.openai.com/codex/config-reference)
- [Agent approvals and security](https://developers.openai.com/codex/security)
- [Codex app and worktrees](https://openai.com/index/introducing-the-codex-app/)
- [Running Codex safely](https://openai.com/index/running-codex-safely/)
- [Codex upgrades: sandbox and verification](https://openai.com/index/introducing-upgrades-to-codex/)
