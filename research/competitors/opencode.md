# OpenCode

**Status:** competitor research

**Last checked:** 2026-09-13

## What it is

OpenCode is an open-source, provider-neutral coding agent with terminal, desktop, and client/server-oriented surfaces. Its public configuration centers on agents, tools, permissions, providers, sessions, and plugins.

## Architecture evidence

- **Agents/loop:** primary agents own the interactive role; subagents create child sessions with separate prompts, models, and permissions. Hidden agents perform compaction, titles, and summaries.
- **Context/state:** `AGENTS.md` supplies scoped repository instructions. Sessions and parent/child navigation preserve task structure; automatic compaction manages long history.
- **Tools:** built-ins include repository search, file changes, shell, web, LSP, and task delegation. Custom TypeScript tools and MCP servers extend the catalog.
- **Permissions:** allow/ask/deny policies apply globally and per agent, with glob-pattern rules for tool/action classes and external directories.
- **Execution:** the shell operates in the selected project/location; permissions control invocation. Public user docs reviewed here do not establish a general OS isolation boundary equivalent to a microVM sandbox.
- **Extensibility:** configured agents plus project/global JS/TS or npm plugins. Plugins can add tools and observe/modify lifecycle events. Fast-moving V2 specifications show a more explicit session/location/tool-registry core, but should not be treated as stable released behavior without version checks.

## Strengths

- Fine-grained, agent-specific tool permissions and easy provider/tool customization.
- Child-session UX makes delegation structure visible.
- Open implementation and plugin surface support inspection and experimentation.

## Trade-offs and unknowns

- Permission decisions are not the same as sandbox enforcement; deployments need a separate isolation story for untrusted execution.
- Rapid evolution and parallel docs/spec versions make current contracts easy to misstate.
- Plugin code executes with application authority, enlarging supply-chain risk.

## Questions for us

- Is a visible parent/child session tree useful to the eventual user, or only to harness developers?
- Which permission rules can be both understandable and enforceable in a short demo?
- Would plugins be user value or merely an implementation convenience?

## First-party sources

- [OpenCode repository](https://github.com/anomalyco/opencode)
- [Agents](https://opencode.ai/docs/agents)
- [Permissions](https://opencode.ai/docs/permissions)
- [Tools](https://opencode.ai/docs/tools)
- [Plugins](https://opencode.ai/docs/plugins)
- [Repository instructions](https://github.com/anomalyco/opencode/blob/dev/packages/web/src/content/docs/rules.mdx)
