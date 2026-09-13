# Accepted architecture

**Status:** UNDECIDED
**Last reviewed:** 2026-09-13

No product architecture, implementation stack, or component boundary has been selected.

## Known constraints

- The submission must satisfy [`hackathon.md`](hackathon.md), including real Nebius use and an NVIDIA open-source model.
- Executable material lives under `app/`; canonical knowledge and external evidence stay outside it.
- Claims of improved agent or harness behavior require controlled evaluation under [`evaluation.md`](evaluation.md).
- A five-person team and hackathon timeline favor a narrow product surface and low operational overhead.

## Architecture goals

- Make the selected user problem easy to demonstrate and measure.
- Keep security and state transitions explicit at execution boundaries.
- Preserve reproducible inputs, environment identity, actions, and outcomes.
- Introduce replaceable components only where experiments or product requirements justify them.
- Make failure, recovery, and cost observable.

## Unresolved questions

- What is the product and therefore the smallest useful runtime boundary?
- Which capabilities require independent replacement: model, loop, context, tools, sandbox, verifier, or persistence?
- What state must be durable, forkable, replayable, or auditable?
- Does the product need one agent, delegated subtasks, or search over execution branches?
- Which operations require user approval, network policy, or secret isolation?
- Which deployment surface best satisfies the demo and judging constraints?

## Inputs, not decisions

- [`../research/architecture-patterns.md`](../research/architecture-patterns.md)
- [`../research/sandboxes.md`](../research/sandboxes.md)
- [`../research/landscape.md`](../research/landscape.md)

Accepted material decisions will be listed in [`decisions/`](decisions/README.md).
