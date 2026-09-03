# Story: Bloqueo de períodos puntuales

**ID:** CAQ-13
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero bloquear períodos puntuales, para evitar reservas cuando no estoy disponible.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede comprobarse sobre una agenda configurada. |
| Negociable | Sí | El bloqueo está definido; el tratamiento de turnos existentes está abierto. |
| Valiosa | Sí | Evita reservas durante ausencias excepcionales. |
| Estimable | No | La interacción con turnos ya confirmados cambia sustancialmente el alcance. |
| Pequeña | Sí | Cubre alta, consulta y eliminación de una excepción de agenda. |
| Testeable | No | Los nuevos slots son verificables; falta el resultado esperado para turnos existentes. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Crear un bloqueo válido

**Given** que el profesional está autenticado
**And** informa un inicio anterior al fin y, opcionalmente, un motivo
**When** crea el bloqueo
**Then** el sistema lo incorpora a su listado
**And** deja de ofrecer para nuevas reservas los horarios incluidos

### Escenario 2: Rechazar un rango inválido

**Given** que el fin del bloqueo es igual o anterior al inicio
**When** el profesional intenta crearlo
**Then** el sistema rechaza la operación
**And** no altera la disponibilidad pública

### Escenario 3: Eliminar un bloqueo

**Given** que existe un bloqueo del profesional
**When** lo elimina
**Then** el sistema lo retira del listado
**And** vuelve a calcular los horarios futuros que ya no estén bloqueados ni reservados

## Notas de QA

* Probar bloqueos parciales, de día completo y superpuestos entre sí.
* No ejecutar en producción con turnos reales.
* La implementación continúa `Sin verificar`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Rango, motivo opcional y exclusión de horarios | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.3 |
| Consulta, creación y eliminación de bloqueos | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Endpoints |
| No alterar silenciosamente turnos existentes | **Hipótesis** — la documentación mantiene abierta la regla y soporte confirma que actualmente permanecen confirmados |

## Contradicciones detectadas

* Ninguna entre las fuentes; el tratamiento de turnos confirmados dentro del bloqueo no fue definido.

## Preguntas abiertas

* ¿Qué ocurre con los turnos ya confirmados dentro del período bloqueado?
* ¿Se permiten bloqueos superpuestos y bloqueos en el pasado?
* ¿Qué zona horaria rige el inicio y el fin?
