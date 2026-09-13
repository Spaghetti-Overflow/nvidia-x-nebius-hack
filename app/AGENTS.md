# Implementation rules

Before material implementation work, consult `../docs/product.md`, `../docs/architecture.md`, `../docs/evaluation.md`, and `../docs/decisions/`.

- Respect accepted architecture; do not silently introduce a language, framework, runtime, or major component boundary.
- Prefer the simplest implementation that proves accepted behavior.
- Test behavioral changes and report the exact verification performed.
- Keep evaluation tasks, environments, budgets, and result generation reproducible.
- Keep raw/generated runtime artifacts out of canonical knowledge and version control.
- Never commit credentials, tokens, private fixtures, or secret-bearing logs.
- Record material architecture/project choices as ADRs; trivial coding choices do not need one.
