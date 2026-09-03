# Story: Resolución de un conflicto de reserva concurrente

**ID:** CAQ-19
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como cliente final, quiero conservar mis datos si otro cliente toma el horario, para elegir otro sin comenzar de nuevo.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Es el caso concurrente de CAQ-18 y depende de la garantía de unicidad. |
| Negociable | Sí | El resultado funcional está claramente documentado. |
| Valiosa | Sí | Evita reservas dobles y repetir la carga de datos. |
| Estimable | Sí | El conflicto, mensaje, conservación y recarga están definidos. |
| Pequeña | Sí | Atiende un único fallo concurrente. |
| Testeable | Sí | Puede ejecutarse con dos sesiones que confirman el mismo horario. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Confirmación ganadora

**Given** que dos clientes seleccionaron el mismo horario disponible
**When** la primera solicitud válida se confirma
**Then** el sistema crea un único turno `confirmed` para ese profesional y horario

### Escenario 2: Rechazar la confirmación perdedora

**Given** que el horario seleccionado dejó de estar disponible
**When** el segundo cliente intenta confirmar
**Then** el sistema rechaza la reserva
**And** informa que otra persona tomó el horario y solicita elegir otro
**And** actualiza la disponibilidad
**And** conserva el nombre y el correo ya ingresados

### Escenario 3: Mantener la unicidad bajo concurrencia

**Given** que llegan simultáneamente varias confirmaciones para el mismo profesional y horario
**When** finalizan las operaciones
**Then** existe como máximo un turno `confirmed` para ese profesional y horario

## Notas de QA

* Ejecutar concurrencia real desde dos sesiones, no una secuencia manual.
* Verificar UI, respuesta API y persistencia.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-19.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Rechazo, mensaje, actualización y conservación de datos | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-02 |
| Garantía de no superposición | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-01 |
| Riesgo de implementación no transaccional | `.context/Confluence-corporativo/04-notas-tecnicas.md` · La reserva; `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · Horarios y disponibilidad |

## Contradicciones detectadas

* La especificación exige impedir superposiciones; las notas técnicas describen una validación no transaccional y soporte registró duplicados. Se conserva la regla funcional y se señala el riesgo de implementación.

## Preguntas abiertas

* ¿Cuál es el texto literal y accesible del mensaje de conflicto?
* ¿Cuánto tiempo se conservan el nombre y el correo después del conflicto?
* ¿La garantía de unicidad se aplica también a altas manuales y reintentos?
