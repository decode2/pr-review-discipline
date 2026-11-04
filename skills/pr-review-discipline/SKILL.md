---
name: pr-review-discipline
description: "Trigger: auditar PR, revisar PR o diff, evaluar solución, abrir/crear PR, push, merge, aprobar issue, status:approved, PRs de la comunidad, fijate este cambio. Approval-first, cinco-vías, QoL, achicabilidad y costos antes de push y merge."
license: Apache-2.0
metadata:
  author: "Gentleman-Programming"
  version: "1.5"
---

## Activation Contract

Load when auditing, reviewing, or evaluating ANY PR or solution pushable to a repository — however the request is phrased ("fijate este cambio", "mirá el diff", "qué opinas") — and before ANY push of own work, PR creation, merge decision, or `status:approved`. If code is about to reach a shared repository, this skill is already active: say so out loud and run its gates.

## Hard Rules

- **Approval precedes work.** An issue without `status:approved` gets an approval evaluation FIRST (reproduction, root cause, scope) and an explicit human decision BEFORE implementing. Never self-approve your own fresh issue to unblock your own PR.
- **Community PRs before own PRs.** Before creating a PR for an issue, search open PRs (all authors) touching it or its files; review and coordinate there first. Open your own only when none covers the need or the author declines theirs.
- **Judge the solution, never the CI.** Green checks are necessary, never sufficient. "Funciona lo que hicieron" is not a merge reason.
- **No fix may create a worse product.** Solving the stated problem while degrading defaults, flow, latency, or error quality is not done.
- **Every fix lands at its smallest honest shape.** Diff weight the fix does not need is requested out before merge, hunks named.
- **Every verdict is a balanced, costed package.** Reasons FOR and AGAINST accepting, with the cost on each axis, are mandatory — even for clear calls. A reject without a proposed more appropriate solution is incomplete.

## Evaluation Method (summary)

Before merge, run the five-fold evaluation and the cost balance in full. The complete methodology — evidence requirements, per-item evaluation questions, and the verdict-package format — lives in `references/five-fold-evaluation.md`.

1. **Problem–solution fit.** Reproduce the claimed problem, apply the PR, verify it is gone — on a fresh PR-head build.
2. **Over-engineering.** Solution architecture must not exceed the problem (states, flags, abstractions, a second mechanism beside an existing one).
3. **Side-effects.** Name every behavior added beyond the fix, then evaluate each: negative, neutral, or beneficial — propose concrete removal, hunks named.
4. **User QoL guard.** Before/after as a USER: defaults, prompts, waits, self-service, error actionability.
5. **Shrinkability.** Smallest honest shape: duplicated logic, dead parameters, speculative generality, footprint wider than the root cause.

Then the **cost balance**: evidenced costs on system, user, and product axes, and a verdict package with reasons FOR and AGAINST — both mandatory — handed to the human.

## Decision Gates

| Situation | Action |
|---|---|
| Issue lacks `status:approved`, work requested | Present approval case → wait for explicit approval |
| Own issue, own PR, label added by self | Stop: the approval is void; route to the human |
| Open community PR covers the same issue/files | Review and coordinate there first |
| PR cannot demonstrate its claimed fix | Reject as ineffective — with the proposed better way |
| Machinery beyond the problem, QoL regression, shrinkable fat | Request the change hunks-named; reject on insistence |
| Works and fits, but a simpler design exists | Request it; supersede only on the author's decline |

## Execution Steps

1. **Before work**: verify `status:approved`; if absent, write the approval case and obtain explicit approval. Record who approved and when.
2. **Before PR**: search open community PRs on the issue and its files; review those first.
3. **Before merge**: run the five-fold evaluation plus the cost balance in writing; hand the pros/cons package to the human; merge only on their explicit approval, with ideal-or-improved and green checks.
4. **After merge**: confirm the issue closed, the class tracked, and the user-facing behavior improved as claimed.

## Output Contract

Return: approval state and approver; community-PR search result; the five-fold evaluation; the cost balance; the pros/cons lists; on reject, the proposed better way. The merge decision is the human's.

## References

- `references/five-fold-evaluation.md` — full five-fold evaluation and verdict-package methodology.
