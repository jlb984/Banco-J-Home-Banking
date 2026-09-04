# Story: Recordatorio del día anterior

**ID:** BJHB-26
**Epic:** BJHB-5
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)
**Estado:** Refinado

## Descripción

Como cliente final, quiero recibir un recordatorio el día anterior, para reducir el riesgo de olvidar el turno.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede procesar turnos ya existentes. |
| Negociable | Sí | El objetivo está definido; momento, zona y reintentos quedan abiertos. |
| Valiosa | Sí | Reduce ausencias por olvido. |
| Estimable | No | No se definieron hora de ejecución ni zona horaria. |
| Pequeña | Sí | Cubre un recordatorio automático previo. |
| Testeable | No | No puede determinarse qué turnos pertenecen a «el día anterior» sin zona y hora acordadas. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Recordar un turno confirmado del día siguiente

**Given** que existe un turno `confirmed` que ocurre al día siguiente según la zona horaria acordada
**When** se ejecuta automáticamente el proceso programado
**Then** el sistema envía al cliente un correo de recordatorio antes del turno

### Escenario 2: Excluir un turno cancelado

**Given** que un turno del día siguiente está `cancelled`
**When** se ejecuta el proceso de recordatorios
**Then** el sistema no envía un recordatorio por ese turno

### Escenario 3: Evitar recordatorios duplicados

**Given** que ya se envió el recordatorio de un turno
**When** el proceso vuelve a evaluar el mismo turno
**Then** no envía un segundo recordatorio

## Notas de QA

* Controlar el reloj para probar límites de fecha, cancelaciones y reejecuciones.
* La idempotencia es una hipótesis pendiente.
* La implementación continúa `Sin verificar`; las fuentes indican que quedó fuera del lanzamiento.

## Inspección Shift-Left

**Resultado:** Bloqueante

**Reporte:** `.context/testing/inspections/inspeccion-BJHB-26.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Recordatorio del día anterior al cliente | `.context/Confluence-corporativo/01-minuta-kickoff.md` · Lo técnico; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 7 |
| Brecha confirmada y necesidad de ejecución programada | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · correo del 28/02/2026 |
| Demanda posterior al lanzamiento | `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · Recordatorios |
| Exclusión de turnos cancelados y automatización | **Hipótesis técnica** — se deducen del objetivo y de la necesidad de un proceso programado |
| Evitar un segundo recordatorio | **Hipótesis** — no hay regla documentada de idempotencia |

## Contradicciones detectadas

* La especificación lo exige, pero el hilo del 03/03/2026 y la reunión del 19/05/2026 confirman que se excluyó del lanzamiento. Se conserva como requisito pendiente, no como comportamiento implementado.

## Preguntas abiertas

* ¿A qué hora y en qué zona horaria se determina «el día anterior»?
* ¿Cuántos reintentos se permiten y cómo se evitan duplicados?
* ¿Qué datos del turno debe incluir el recordatorio?
