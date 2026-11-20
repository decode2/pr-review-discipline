---
name: pr-review-discipline
description: "Trigger: auditar PR, revisar diff, antes de push, PR o merge, aprobar issue, status:approved. Approval-first, seis-vías, QoL, achicabilidad, valor de tests, costos. / Audit a PR or diff, before push or merge. Six-fold review, QoL, test value, costed verdicts."
license: Apache-2.0
metadata:
  author: "decode2"
  version: "1.7"
---

## Activation Contract / Contrato de activación

Load when auditing, reviewing, or evaluating ANY PR or diff pushable to a repository — however the request is phrased ("fijate este cambio", "mirá el diff", "qué opinas") — and before ANY push of own work, PR creation, merge decision, or `status:approved`. If code is about to reach a shared repository, this skill is already active: say so out loud and run its gates.

Se activa al auditar, revisar o evaluar CUALQUIER PR o diff que pueda llegar a un repositorio — como sea que se pida ("fijate este cambio", "mirá el diff", "qué opinas") — y antes de CUALQUIER push de trabajo propio, creación de PR, decisión de merge o `status:approved`. Si el código está por llegar a un repositorio compartido, este skill ya está activo: decilo en voz alta y corré sus compuertas.

## Hard Rules / Reglas duras

- **Approval precedes work.** An issue without `status:approved` gets an approval evaluation FIRST and an explicit human decision BEFORE implementing. Never self-approve your own fresh issue. / **La aprobación precede al trabajo.** Un issue sin `status:approved` recibe PRIMERO la evaluación de aprobación y una decisión humana explícita ANTES de implementar. Nunca te auto-apruebes un issue propio.
- **Community PRs before own PRs.** Before creating a PR for an issue, search open PRs (all authors) touching it or its files; review and coordinate there first. / **PRs de la comunidad antes que los propios.** Antes de crear un PR para un issue, buscá PRs abiertos (de cualquier autor) que lo toquen; revisá y coordiná allí primero.
- **Judge the solution, never the CI.** Green checks are necessary, never sufficient. / **Juzgá la solución, nunca el CI.** Los checks verdes son necesarios, nunca suficientes.
- **No fix may create a worse product.** Degrading defaults, flow, latency, or error quality is not done. / **Ningún arreglo puede crear un producto peor.** Degradar defaults, flujo, latencia o calidad de errores no está permitido.
- **Every fix lands at its smallest honest shape.** Unneeded diff weight is requested out before merge, hunks named. / **Todo arreglo llega a su forma honesta más pequeña.** El peso de diff innecesario se pide fuera antes del merge, con hunks nombrados.
- **Tests must earn their place.** What enters the repo carries tests per the repo's own criteria, and every test proves a real case of this change. Tests written only because TDD or a checklist demanded them are not coverage. / **Los tests tienen que ganarse su lugar.** Lo que entra al repo lleva tests según el criterio del propio repo, y cada test prueba un caso real de este cambio. Los tests escritos solo porque TDD o un checklist los pedía no son cobertura.
- **Every verdict is a balanced, costed package.** Reasons FOR and AGAINST, both mandatory, even for clear calls. A reject without a proposed better solution is incomplete. / **Todo veredicto es un paquete balanceado y costeado.** Razones a FAVOR y en CONTRA, ambas obligatorias, incluso en llamadas claras. Un rechazo sin solución mejor propuesta está incompleto.

## Evaluation Method / Método de evaluación

Before merge, run the six-fold evaluation and the cost balance in full — methodology in `references/six-fold-evaluation.md`. / Antes del merge, corré la evaluación de seis vías y el balance de costos completos — metodología en `references/six-fold-evaluation.md`.

1. **Problem–solution fit.** Reproduce the problem, apply the PR, verify it is gone. / **Ajuste problema–solución.** Reproducí el problema, aplicá el PR, verificá que desapareció.
2. **Over-engineering.** Architecture must not exceed the problem. / **Sobre-ingeniería.** La arquitectura no debe exceder el problema.
3. **Side-effects.** Name each behavior added, then evaluate it; propose removal hunks-named. / **Efectos secundarios.** Nombrá cada comportamiento agregado y evalualo; proponé remoción con hunks nombrados.
4. **User QoL guard.** Before/after as a USER: defaults, prompts, waits, errors. / **Guardia de QoL.** Antes/después como USUARIO: defaults, prompts, esperas, errores.
5. **Shrinkability.** Smallest honest shape: duplicated logic, dead parameters, speculative generality. / **Achicabilidad.** La forma honesta más pequeña: lógica duplicada, parámetros muertos, generalidad especulativa.
6. **Test value.** Tests exist per the repo's criteria, and each one proves real behavior of this change, the right way; ritual tests are named and fixed. / **Valor de los tests.** Hay tests según el criterio del repo, y cada uno prueba comportamiento real de este cambio, de la forma adecuada; los tests de ritual se nombran y se corrigen.

Then the **cost balance**: evidenced costs on system, user, and product axes; verdict package with reasons FOR and AGAINST — both mandatory — for the human. / Luego el **balance de costos**: costos evidenciados en ejes sistema, usuario y producto; paquete de veredicto con razones a FAVOR y en CONTRA — ambas obligatorias — para el humano.

## Decision Gates / Compuertas de decisión

| Situation / Situación | Action / Acción |
|---|---|
| Issue lacks `status:approved` / Issue sin `status:approved` | Present approval case → wait for explicit approval / Presentar el caso → esperar aprobación explícita |
| Own issue, own PR, self-added label / Issue propio, PR propio, label auto-agregada | Stop: approval is void; route to the human / Detener: la aprobación es nula; escalar al humano |
| Open community PR covers the same files / PR comunitario abierto cubre los mismos archivos | Review and coordinate there first / Revisar y coordinar allí primero |
| PR cannot demonstrate its fix / El PR no puede demostrar su arreglo | Reject as ineffective, with the better way / Rechazar como inefectivo, con la vía mejor |
| Machinery beyond problem, QoL regression, shrinkable fat / Maquinaria de más, regresión de QoL, grasa achicable | Request change hunks-named; reject on insistence / Pedir el cambio con hunks; rechazar si insiste |
| Change lacks the tests the repo's criteria require / Al cambio le faltan los tests que exige el criterio del repo | Request them, naming the behaviors to cover / Pedirlos, nombrando los comportamientos a cubrir |
| Tests pass but prove nothing real (ritual, tautological, mock-only, wrong level) / Los tests pasan pero no prueban nada real (ritual, tautológicos, solo mocks, nivel equivocado) | Request rewrite or removal, tests named, with the case each should prove / Pedir reescritura o remoción, con tests nombrados y el caso que cada uno debería probar |
| Works, but a simpler design exists / Funciona, pero existe un diseño más simple | Request it; supersede only on author's decline / Pedirlo; imponer solo si el autor declina |

## Execution Steps / Pasos de ejecución

1. **Before work / Antes de trabajar**: verify `status:approved`; if absent, write the approval case, obtain explicit approval, record who and when. / verificá `status:approved`; si falta, escribí el caso de aprobación, obtené aprobación explícita, registrá quién y cuándo.
2. **Before PR / Antes del PR**: search open community PRs on the issue and its files; review those first. / buscá PRs comunitarios abiertos sobre el issue y sus archivos; revisá esos primero.
3. **Before merge / Antes del merge**: run the six-fold evaluation plus cost balance in writing; hand the pros/cons package to the human; merge only on explicit approval. / corré la evaluación de seis vías más el balance de costos por escrito; entregá el paquete de pros/contras al humano; merge solo con aprobación explícita.
4. **After merge / Después del merge**: confirm the issue closed, the class tracked, the user-facing behavior improved. / confirmá el issue cerrado, la clase rastreada, el comportamiento de usuario mejorado.

## Output Contract / Contrato de salida

Return: approval state and approver; community-PR search result; six-fold evaluation; cost balance; pros/cons lists; on reject, the proposed better way. The merge decision is the human's. / Devolver: estado de aprobación y aprobador; resultado de búsqueda de PRs comunitarios; evaluación de seis vías; balance de costos; listas de pros/contras; en rechazo, la vía mejor propuesta. La decisión de merge es del humano.

## References / Referencias

- `references/six-fold-evaluation.md` — full methodology / metodología completa.
