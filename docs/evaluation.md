# Evaluation philosophy

**Status:** initial team policy
**Last reviewed:** 2026-09-13

Product and architecture claims must be falsifiable. A statement such as “our harness is better” is incomplete until it names a user-relevant task, baseline, controlled variables, metric, and acceptance threshold.

## Comparison contract

When comparing harness strategies, hold constant where possible:

```text
same model + same task + same starting environment + same budget
different harness strategy
```

Record unavoidable differences and avoid causal claims when multiple variables changed. Use more than one run when model sampling or infrastructure introduces variance. Preserve failures; do not report only successful trials.

## Candidate measures

| Outcome | Efficiency | Reliability/diagnosis |
|---|---|---|
| Task success rate | Input/output tokens | Failed actions |
| Tests or acceptance checks passed | Wall-clock/model latency | Recovery behavior |
| User workflow completion | Cost and model calls | Reproducibility across runs |
| Patch/product quality rubric | Tool calls / executed work | Policy violations and unsafe attempts |

Metrics are selected per product claim; collecting every metric is not a goal. Automated judges must be calibrated against deterministic checks or human review.

## Evaluation workspace

[`../app/evals/`](../app/evals/README.md) will hold versioned task definitions, baselines, fixtures, and curated reports. Raw runs are generated and ignored. Every curated report should identify the code revision, model, prompts/configuration, environment or image, budget, task set, seeds when available, and evaluator version.
