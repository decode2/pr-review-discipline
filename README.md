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
├── SKILL.md                              # runtime instruction contract
└── references/
    └── five-fold-evaluation.md           # full pre-merge methodology
```

## What it enforces

- Approval precedes work — no self-approving your own issue to unblock your own PR.
- Community PRs before own PRs — review and coordinate there first.
- Judge the solution, never the CI — green checks are necessary, never sufficient.
- No fix may create a worse product — QoL regressions are argued or reverted.
- Every fix lands at its smallest honest shape — shrink requests are hunks-named.
- Every verdict is a balanced, costed package — reasons FOR and AGAINST, costs on system/user/product axes, and a proposed better way on reject.

## Companion skills

Works alongside `systemic-issue-triage` (root-class grouping, over-engineering gate) and `branch-pr` (mechanical PR creation after these gates pass), available in the [Gentleman-Programming](https://github.com/Gentleman-Programming) skill collections.

## License

Apache-2.0
