# pr-review-discipline

![pr-review-discipline banner](assets/banner.png)

An AI agent skill for disciplined pull-request review and merge decisions.

Approval-first workflow: issues get an explicit human approval before implementation, community PRs are reviewed before opening your own, and every merge decision runs a five-fold evaluation (problem–solution fit, over-engineering, side-effects, user QoL guard, shrinkability) plus an evidenced cost balance — handed to the human as a pros/cons package. The merge decision is always the human's.

## Install

```bash
npx skills add decode2/pr-review-discipline
```

## Structure

```
skills/pr-review-discipline/
├── SKILL.md                              # runtime instruction contract (EN/ES)
└── references/
    └── five-fold-evaluation.md           # full pre-merge methodology (EN/ES)
```

## Qué aplica / What it enforces

- Approval precedes work / La aprobación precede al trabajo — no self-approving your own issue to unblock your own PR.
- Community PRs before own PRs / PRs comunitarios antes que los propios — review and coordinate there first.
- Judge the solution, never the CI / Juzgá la solución, nunca el CI — green checks are necessary, never sufficient.
- No fix may create a worse product / Ningún arreglo crea un producto peor — QoL regressions are argued or reverted.
- Every fix lands at its smallest honest shape / Todo arreglo llega a su forma más pequeña — shrink requests are hunks-named.
- Every verdict is a balanced, costed package / Todo veredicto es un paquete costeado — reasons FOR and AGAINST, costs on system/user/product axes, and a proposed better way on reject.

## Compatibilidad / Compatibility

The skill instructions are written in English and Spanish — agents can run it from either language. Triggers cover both ("auditar PR", "fijate este cambio", "audit a PR", "review this diff").

Designed for the Gentle skill format (Activation Contract, Hard Rules, Decision Gates); works in Gentle Shell and any agent runtime that loads `SKILL.md` skills. Pairs naturally with `systemic-issue-triage` (root-class grouping, over-engineering gate) and `branch-pr` (mechanical PR creation after these gates pass).

## License

Apache-2.0
