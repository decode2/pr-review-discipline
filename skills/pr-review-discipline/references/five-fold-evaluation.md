# Five-fold Evaluation and Verdict Package

Full methodology for the `pr-review-discipline` skill. Load when running the pre-merge evaluation.

## The five-fold evaluation (mandatory before merge)

1. **Problem–solution fit.** Reproduce the claimed problem, apply the PR, verify it is gone — on a fresh PR-head build. No demonstrated fix = ineffective.
2. **Over-engineering.** Does the SOLUTION ARCHITECTURE exceed the problem: states, flags, abstractions, a second mechanism beside an existing one, machinery whose only consumer is its own test path? Request reduction or reject.
3. **Side-effects.** Name every behavior the diff adds beyond the stated fix: new failure modes, dead ends without executable exits, silent-loss paths, masking errors, scope creep. Then evaluate each named side effect instead of just listing it: is it negative, neutral, or does it carry its own benefit? Does it conflict with another behavior, mechanism, or contract in the repo (including test suites, budgets, and ratchets)? If it is avoidable or negotiable, the review proposes the concrete change that removes it (hunks named) instead of accepting it silently; if it stays, the cost of keeping it is stated in the verdict package.
4. **User QoL guard.** Before/after as a USER: defaults, prompts, waits, self-service, error actionability. Hidden changes smuggled under another headline are argued or reverted.
5. **Shrinkability.** Is the diff the smallest shape that fulfills the fix? Hunt duplicated logic, verbose constructs where a repo/stdlib util exists, dead parameters, speculative generality, deletable hunks, footprint wider than the root cause. Tests, docs, registries, fail-open guards are contract, not fat. Request the shrink hunks-named.

## The cost balance and the verdict package (mandatory in every review)

Costs on three axes, evidenced:

- **system** — maintenance, complexity debt, performance, security surface, coupling
- **user** — QoL plus migration and behavior-change costs
- **product** — support burden, dependency weight, roadmap fit

Then the package for the human: reasons FOR and AGAINST accepting — both mandatory, both evidenced, even for obvious calls. The human decides with the full picture; the reviewer never hides a cost to steer it. On reject: propose the more appropriate solution (named approach, reframe, or the existing mechanism that fits) — a bare no is incomplete.
