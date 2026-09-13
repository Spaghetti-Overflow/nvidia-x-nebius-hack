# Aider

**Status:** competitor research

**Last checked:** 2026-09-13

## What it is

Aider is an open-source terminal pair programmer tightly integrated with a local Git repository. Its central architectural bets are high-signal repository context and model-specific edit protocols, with a human kept in the interactive loop.

## Architecture evidence

- **Context:** users select editable/read-only files. A graph-ranked repository map uses tree-sitter tags and dependency relationships to fit important symbols into a token budget.
- **Edit protocol:** model-specific formats include whole-file, search/replace diff, and unified-diff variants. Architect mode can separate a reasoning model from an editor model.
- **State:** chat history plus the Git working tree/commits form the practical record. Aider auto-commits its edits by default, isolates pre-existing dirty changes, and provides `/diff` and `/undo`.
- **Execution/verification:** commands run in the user's environment. Edited files auto-lint by default; configured tests can run automatically or via `/test`, and failing output is offered back for repair.
- **Models/extensibility:** a main, weak, and optional editor model; prompts, edit/coder classes, commands, conventions, and extensive configuration are customizable. It is not primarily a general plugin runtime.

## Strengths

- Repository map is a concrete solution to global structure under a small context budget.
- Edit formats acknowledge that the ACI should match model behavior.
- Git-native checkpoints make human review and reversal simple.

## Trade-offs

- Local command execution is not an isolation boundary.
- Git commits capture repository files, not full environment/process state or a complete causal trajectory.
- Interactive pair-programming assumptions differ from unattended multi-step agents and branch search.

## Questions for us

- Is the eventual bottleneck codebase navigation, edit reliability, execution evidence, or something else?
- Would Git state be sufficient, or must dependencies and filesystem mutations branch with code?
- Can a small model-specific ACI beat a generic tool catalog under controlled evaluation?

## First-party sources

- [Repository map](https://aider.chat/docs/repomap.html)
- [Edit formats](https://aider.chat/docs/more/edit-formats.html)
- [Git integration](https://aider.chat/docs/git.html)
- [Linting and testing](https://aider.chat/docs/usage/lint-test.html)
- [Source repository](https://github.com/Aider-AI/aider)
