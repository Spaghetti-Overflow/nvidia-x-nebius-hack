# Evaluation workspace

This subtree will implement the policy in [`../../docs/evaluation.md`](../../docs/evaluation.md). It contains no invented tasks, baselines, or results.

| Path | Contract |
|---|---|
| `tasks/` | Versioned task definitions, acceptance criteria, and task metadata |
| `baselines/` | Reproducible comparison configurations; never favorable strawmen |
| `fixtures/` | Small, licensed, non-secret inputs required by tasks |
| `reports/` | Curated, human-readable results with provenance; suitable for versioning |
| `runs/` | Raw/generated trajectories, logs, sandbox artifacts, and machine output; gitignored |

Every report should identify the code revision, task/baseline versions, model and provider identifier, prompts/harness config, environment/image, budgets, repetitions or seeds, evaluator version, failures, and the command/workflow that generated it. Do not manually edit raw runs into apparent evidence.
