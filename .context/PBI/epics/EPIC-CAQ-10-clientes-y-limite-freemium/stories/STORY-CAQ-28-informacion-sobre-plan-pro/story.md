# Story: Información sobre el Plan Pro al alcanzar el límite

**ID:** CAQ-28
**Epic:** CAQ-10
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional que alcanzó el límite, quiero recibir información clara sobre el Plan Pro, para conocer mis opciones.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende de que CAQ-27 detecte el límite. |
| Negociable | Sí | Comunicación y CTA están definidas; oferta comercial queda fuera. |
| Valiosa | Sí | Explica la continuidad del plan y registra intención de conversión. |
| Estimable | No | No se definió cómo se registra ni gestiona el interés. |
| Pequeña | Sí | Cubre correo, aviso y CTA ante un evento concreto. |
| Testeable | Sí | Disparo, persistencia del aviso y ausencia de cobro son verificables. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Informar al alcanzar diez clientes únicos

**Given** que el profesional alcanza diez clientes únicos
**When** el sistema procesa ese evento
**Then** envía al profesional un correo con tono de celebración
**And** muestra en su panel un aviso permanente
**And** explica que sus clientes actuales pueden seguir reservando

### Escenario 2: Solicitar más información

**Given** que el profesional ve el aviso del límite
**When** selecciona «Más información sobre el Plan Pro»
**Then** el sistema registra su interés
**And** no ejecuta un cobro ni confirma una contratación

### Escenario 3: Mantener visible el aviso

**Given** que el profesional ya alcanzó el límite
**When** vuelve a ingresar a su panel
**Then** el aviso sobre el Plan Pro continúa visible

## Notas de QA

* Verificar que el correo se dispare una sola vez por el evento de alcanzar el límite.
* No evaluar precio ni beneficios como criterio hasta que exista una definición.
* La implementación continúa `Sin verificar`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Correo y aviso permanente en el panel | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.2 |
| Texto vigente de la llamada a la acción | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · resumen del 03/03/2026 |
| Registro de interés sin plan pago | `.context/Confluence-corporativo/01-minuta-kickoff.md` · El modelo: freemium; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.3 |
| Precio, beneficios y cobro | **Pregunta abierta** — el Plan Pro no existe como oferta definida |
| Envío único del correo por evento | **Hipótesis** — no hay regla documentada sobre reintentos o duplicados |

## Contradicciones detectadas

* El concepto de Plan Pro existe como llamada a la acción, pero no como oferta con precio, beneficios o contratación definidos. Se limita el alcance a informar y registrar interés.

## Preguntas abiertas

* ¿Dónde y con qué datos se registra el interés?
* ¿Qué texto exacto y contenido debe tener el correo y el aviso?
* ¿Cuándo deja de mostrarse el aviso y cómo se evitan correos duplicados?
