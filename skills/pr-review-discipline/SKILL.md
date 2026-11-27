---
name: pr-review-discipline
description: "Trigger: audit a PR, review a diff, before push, PR, or merge, approve an issue, status:approved; also auditar PR, revisar diff, fijate este cambio, mirá el diff. Six-fold review, QoL, test value, costed verdicts, optional approval gates."
license: Apache-2.0
metadata:
  author: "decode2"
  version: "1.10"
---

## Activation Contract

Load when auditing, reviewing, or evaluating ANY PR or diff pushable to a repository — however the request is phrased, in any language ("review this diff", "fijate este cambio", "mirá el diff", "qué opinas") — and before ANY push of own work, PR creation, merge decision, or `status:approved`. If code is about to reach a shared repository, this skill is already active: say so out loud and run its gates.

## Language Contract

- These instructions are written in English; they apply in full whatever language the conversation uses.
- Reply to the user in the language of their latest message. Write the evaluation, cost balance, verdict package, and every question in that language.
- Keep the skill's fixed terms recognizable: gate names, labels such as `status:approved`, file paths, commands, and code stay as written; translate the explanation around them.
- Public artifacts (PR comments, review comments, commit messages) follow the target repository's language unless the user asks otherwise.

## Workflow Detection

Two gates are optional: they apply only when the repository works that way. Detect it before the first gate, state the result, and skip what does not apply.

- **Approval gate** — applies when the repo runs issue-first approval: a `status:approved` (or equivalent) label exists, or CONTRIBUTING, the PR template, or CI requires a linked approved issue, or the human asks for it.
- **Community-PR gate** — applies when the repo takes outside contributions: it is public and has open or recent PRs from other authors, or the human asks for it. Private or single-maintainer repos skip it.
- **Unclear evidence** — ask the human once; never block work on a gate the repo does not use.

## Hard Rules

- **Approval precedes work (when the approval gate applies).** An issue without `status:approved` gets an approval evaluation FIRST and an explicit human decision BEFORE implementing. Never self-approve your own fresh issue.
- **Community PRs before own PRs (when the community-PR gate applies).** Before creating a PR for an issue, search open PRs (all authors) touching it or its files; review and coordinate there first.
- **Judge the solution, never the CI.** Green checks are necessary, never sufficient.
- **No fix may create a worse product.** Degrading defaults, flow, latency, or error quality is not done.
- **Every fix lands at its smallest honest shape.** Unneeded diff weight is requested out before merge, hunks named.
- **Tests must earn their place.** What enters the repo carries tests per the repo's own criteria, and every test proves a real case of this change. Tests written only because TDD or a checklist demanded them are not coverage.
- **Every verdict is a balanced, costed package.** Reasons FOR and AGAINST, both mandatory, even for clear calls. A reject without a proposed better solution is incomplete.

## Evaluation Method

Before merge, run the six-fold evaluation and the cost balance in full — methodology in `references/six-fold-evaluation.md`.

1. **Problem–solution fit.** Reproduce the problem, apply the PR, verify it is gone. Failure observed = ineffective; proof missing = pending, naming the proof.
2. **Over-engineering.** Architecture must not exceed the problem.
3. **Side-effects.** Name each behavior added, then evaluate it; propose removal hunks-named.
4. **User QoL guard.** Before/after as a USER: defaults, prompts, waits, errors.
5. **Shrinkability.** Smallest honest shape: duplicated logic, dead parameters, speculative generality.
6. **Test value.** Tests exist per the repo's criteria, and each one proves real behavior of this change, the right way; ritual tests are named and fixed.

Then the **cost balance**: evidenced costs on system, user, and product axes; verdict package with reasons FOR and AGAINST — both mandatory — for the human.

## Decision Gates

| Situation | Action |
|---|---|
| Repo does not use an optional gate | Skip it and say why in the output |
| Approval gate applies, issue lacks `status:approved` | Present approval case → wait for explicit approval |
| Approval gate applies: own issue, own PR, self-added label | Stop: approval is void; route to the human |
| Community-PR gate applies, open PR covers the same files | Review and coordinate there first |
| Fix tested on the commit under review and the problem persists | Reject as ineffective, document the observed failure, with the better way |
| Proof required to decide is missing (any environment) | Record which proof is missing; keep the merge pending |
| Author or another reviewer supplied evidence for the commit | Evaluate it against the project's criteria; continue if it meets them |
| Machinery beyond problem, QoL regression, shrinkable fat | Request change hunks-named; reject on insistence |
| Change lacks the tests the repo's criteria require | Request them, naming the behaviors to cover |
| Tests pass but prove nothing real (ritual, tautological, mock-only, wrong level, green under a plausible regression) | Request rewrite or removal, tests named, with the case each should prove |
| Works, but a simpler design exists | Request it; supersede only on author's decline |

## Execution Steps

0. **Detect workflow**: decide which optional gates apply (see Workflow Detection) and state it.
1. **Before work** (approval gate only): verify `status:approved`; if absent, write the approval case, obtain explicit approval, record who and when.
2. **Before PR** (community-PR gate only): search open community PRs on the issue and its files; review those first.
3. **Before merge**: run the six-fold evaluation plus cost balance in writing; hand the pros/cons package to the human; merge only on explicit approval.
4. **After merge**: confirm the user-facing behavior improved and, when there is an issue, that it closed and its class is tracked.

## Output Contract

Return, in the user's language: which optional gates apply and why; approval state and approver, or "not applicable"; community-PR search result, or "not applicable"; six-fold evaluation; cost balance; pros/cons lists; on reject, the proposed better way. The merge decision is the human's.

## References

- `references/six-fold-evaluation.md` — full methodology.
