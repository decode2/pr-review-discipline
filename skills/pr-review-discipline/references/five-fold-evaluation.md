# Five-fold Evaluation and Verdict Package / Evaluación de cinco vías y paquete de veredicto

Full methodology for the `pr-review-discipline` skill. Load when running the pre-merge evaluation.
Metodología completa del skill `pr-review-discipline`. Cargala al correr la evaluación previa al merge.

## The five-fold evaluation / La evaluación de cinco vías (mandatory / obligatoria before merge)

1. **Problem–solution fit / Ajuste problema–solución.** Reproduce the claimed problem, apply the PR, verify it is gone — on a fresh PR-head build. No demonstrated fix = ineffective. / Reproducí el problema reclamado, aplicá el PR, verificá que desapareció — sobre un build fresco de la cabeza del PR. Arreglo no demostrado = inefectivo.
2. **Over-engineering / Sobre-ingeniería.** Does the SOLUTION ARCHITECTURE exceed the problem: states, flags, abstractions, a second mechanism beside an existing one, machinery whose only consumer is its own test path? Request reduction or reject. / ¿La ARQUITECTURA de la solución excede el problema: estados, flags, abstracciones, un segundo mecanismo junto a uno existente, maquinaria cuyo único consumidor es su propio camino de tests? Pedí reducción o rechazá.
3. **Side-effects / Efectos secundarios.** Name every behavior the diff adds beyond the stated fix: new failure modes, dead ends without executable exits, silent-loss paths, masking errors, scope creep. Then evaluate each: negative, neutral, or beneficial? Does it conflict with another mechanism or contract in the repo (test suites, budgets, ratchets)? If avoidable, propose the concrete change that removes it (hunks named); if it stays, state its cost in the verdict package. / Nombrá cada comportamiento que el diff agrega más allá del arreglo: nuevos modos de falla, callejones sin salida ejecutable, caminos de pérdida silenciosa, errores enmascarados, scope creep. Después evaluala cada uno: ¿negativo, neutro o con beneficio propio? ¿Conflicta con otro mecanismo o contrato del repo (suites de tests, budgets, ratchets)? Si es evitable, proponé el cambio concreto que lo remueve (hunks nombrados); si queda, declará su costo en el paquete de veredicto.
4. **User QoL guard / Guardia de QoL.** Before/after as a USER: defaults, prompts, waits, self-service, error actionability. Hidden changes smuggled under another headline are argued or reverted. / Antes/después como USUARIO: defaults, prompts, esperas, autoservicio, accionabilidad de errores. Los cambios ocultos colados bajo otro titular se argumentan o se revierten.
5. **Shrinkability / Achicabilidad.** Is the diff the smallest shape that fulfills the fix? Hunt duplicated logic, verbose constructs where a repo/stdlib util exists, dead parameters, speculative generality, deletable hunks, footprint wider than the root cause. Tests, docs, registries, fail-open guards are contract, not fat. / ¿Es el diff la forma más pequeña que cumple el arreglo? Cazá lógica duplicada, constructos verbosos donde existe un util del repo/stdlib, parámetros muertos, generalidad especulativa, hunks eliminables, huella más ancha que la causa raíz. Tests, docs, registros y guardas fail-open son contrato, no grasa.

## The cost balance and the verdict package / El balance de costos y el paquete de veredicto (mandatory in every review / obligatorio en toda revisión)

Costs on three axes, evidenced / Costos en tres ejes, evidenciados:

- **system / sistema** — maintenance, complexity debt, performance, security surface, coupling / mantenimiento, deuda de complejidad, performance, superficie de seguridad, acoplamiento
- **user / usuario** — QoL plus migration and behavior-change costs / QoL más costos de migración y cambio de comportamiento
- **product / producto** — support burden, dependency weight, roadmap fit / carga de soporte, peso de dependencias, encaje en el roadmap

Then the package for the human: reasons FOR and AGAINST accepting — both mandatory, both evidenced, even for obvious calls. The human decides with the full picture; the reviewer never hides a cost to steer it. On reject: propose the more appropriate solution (named approach, reframe, or the existing mechanism that fits) — a bare no is incomplete.

Luego el paquete para el humano: razones a FAVOR y en CONTRA de aceptar — ambas obligatorias, ambas evidenciadas, incluso en llamadas obvias. El humano decide con el cuadro completo; el revisor nunca oculta un costo para inclinar la balanza. En rechazo: proponé la solución más apropiada (enfoque nombrado, reencuadre, o el mecanismo existente que encaja) — un no pelado está incompleto.
