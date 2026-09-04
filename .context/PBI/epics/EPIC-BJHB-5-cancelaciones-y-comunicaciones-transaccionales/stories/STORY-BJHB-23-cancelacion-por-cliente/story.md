# Story: Cancelación por el cliente mediante enlace

**ID:** BJHB-23
**Epic:** BJHB-5
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)
**Estado:** Refinado

## Descripción

Como cliente final, quiero cancelar mediante el enlace de mi correo, para liberar el horario sin crear una cuenta.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende del correo de confirmación y su enlace único. |
| Negociable | Sí | El objetivo y efectos están definidos; la ventana de cancelación queda abierta. |
| Valiosa | Sí | Permite liberar el horario sin crear una cuenta. |
| Estimable | No | No se definieron vigencia, reutilización ni respuesta del enlace. |
| Pequeña | Sí | Cubre una cancelación iniciada por el cliente. |
| Testeable | Sí | Estado, autorización por token y liberación pueden comprobarse. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Cancelar un turno futuro mediante enlace

**Given** que el cliente posee el enlace único de un turno futuro `confirmed`
**When** abre el enlace y confirma la cancelación sin iniciar sesión
**Then** el sistema cambia el turno a `cancelled`
**And** vuelve a ofrecer el horario según las reglas vigentes

### Escenario 2: Rechazar la cancelación de un turno pasado

**Given** que el enlace corresponde a un turno pasado
**When** el cliente intenta cancelarlo
**Then** el sistema rechaza la operación
**And** no modifica el turno

### Escenario 3: Reutilizar el enlace de un turno ya cancelado

**Given** que el turno del enlace ya está `cancelled`
**When** el cliente vuelve a usarlo
**Then** el sistema no ejecuta una segunda cancelación
**And** no crea ni modifica otros turnos

## Notas de QA

* Probar token válido, alterado, de otro turno y ya utilizado.
* Verificar persistencia y disponibilidad pública después de cancelar.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-BJHB-23.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Enlace único sin cuenta | `.context/Confluence-corporativo/01-minuta-kickoff.md` · Los dos usuarios del sistema; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.1 |
| Restricción temporal, estado y liberación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.3 |
| Riesgo del endpoint público | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Endpoints |
| No repetir efectos al reutilizar un enlace | **Hipótesis** — no hay regla documentada para idempotencia |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿El enlace vence y puede revocarse o regenerarse?
* ¿Existe una ventana mínima previa al turno para cancelar?
* ¿Qué respuesta se muestra ante un token inválido, un turno pasado o ya cancelado?
