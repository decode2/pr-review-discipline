# Six-fold Evaluation and Verdict Package

Full methodology for the `pr-review-discipline` skill. Load when running the pre-merge evaluation. Report results in the user's language, per the skill's Language Contract.

## The six-fold evaluation (mandatory before merge)

1. **Problem–solution fit.** Reproduce the claimed problem, apply the PR, verify it is gone — on a fresh PR-head build. Classify the outcome by the evidence available for the exact commit under review:
   - **Failure observed.** The commit was tested under suitable conditions and the problem persists: declare the fix ineffective and document the observed failure.
   - **Proof missing.** A proof required to decide is absent, whether or not you own the environment (for example, a device-specific bug): record which proof is missing and keep the merge pending. Missing evidence is not a failed fix.
   - **Evidence supplied.** The author or another reviewer provided evidence for that commit: evaluate it against the project's own criteria and continue if it meets them. When the project defines none, default to: it comes from the affected environment, names the commit it ran on, and shows the symptom gone. Otherwise decide, and state the criteria you used.
2. **Over-engineering.** Does the SOLUTION ARCHITECTURE exceed the problem: states, flags, abstractions, a second mechanism beside an existing one, machinery whose only consumer is its own test path? Request reduction or reject.
3. **Side-effects.** Name every behavior the diff adds beyond the stated fix: new failure modes, dead ends without executable exits, silent-loss paths, masking errors, scope creep. Then evaluate each: negative, neutral, or beneficial? Does it conflict with another mechanism or contract in the repo (test suites, budgets, ratchets)? If avoidable, propose the concrete change that removes it (hunks named); if it stays, state its cost in the verdict package.
4. **User QoL guard.** Before/after as a USER: defaults, prompts, waits, self-service, error actionability. Hidden changes smuggled under another headline are argued or reverted.
5. **Shrinkability.** Is the diff the smallest shape that fulfills the fix? Hunt duplicated logic, verbose constructs where a repo/stdlib util exists, dead parameters, speculative generality, deletable hunks, footprint wider than the root cause. Tests that pass the test-value check (6), docs, registries, fail-open guards are contract, not fat.
6. **Test value.** First, presence: read the repo's testing criteria (CONTRIBUTING, existing suites, CI config, conventions for this layer) and check the change carries the tests they require; missing tests are requested with the behaviors to cover named. Then, value — for each test the diff adds or changes, ask:
   - (a) Does it exercise behavior this change introduces, fixes, or must preserve (refactors, characterization tests), or does it only restate the implementation?
   - (b) Would it FAIL if the behavior it protects were broken? For a bugfix, red without the fix wherever reproducing the defect is feasible. For a refactor or characterization test, green on the original code is expected: judge it against a plausible regression instead. A test that stays green when the behavior breaks proves nothing (for example, asserting only a result's type where its value is the contract); type assertions are fine where the type is the contract.
   - (c) Does it model a real case — real inputs, the boundaries and error paths the rule names — rather than a trivial happy path?
   - (d) Is it at the right level and through the public interface, asserting observable effects (output, state, errors), not private calls or mock interactions alone?
   - (e) Is it deterministic and independent of order, time, and network?

   Ritual tests — written because TDD or a checklist demanded them: tautologies, mocks testing mocks, snapshots nobody reads, assertions on constants, coverage padding — are named and requested rewritten toward the real case, or removed. A useless test is not contract; it is cost: it slows the suite and gives false confidence.

## The cost balance and the verdict package (mandatory in every review)

Costs on three axes, evidenced:

- **system** — maintenance, complexity debt, performance, security surface, coupling
- **user** — QoL plus migration and behavior-change costs
- **product** — support burden, dependency weight, roadmap fit

Then the package for the human: reasons FOR and AGAINST accepting — both mandatory, both evidenced, even for obvious calls. The human decides with the full picture; the reviewer never hides a cost to steer it. On reject: propose the more appropriate solution (named approach, reframe, or the existing mechanism that fits) — a bare no is incomplete.
