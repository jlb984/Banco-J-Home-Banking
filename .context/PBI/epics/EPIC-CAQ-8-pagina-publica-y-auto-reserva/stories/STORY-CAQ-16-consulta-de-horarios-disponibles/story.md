# Story: Consulta pública de horarios disponibles

**ID:** CAQ-16
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como cliente final, quiero consultar los horarios disponibles, para elegir una opción conveniente.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | La consulta puede probarse sin confirmar una reserva. |
| Negociable | Sí | Las exclusiones están definidas; navegación y zona horaria quedan abiertas. |
| Valiosa | Sí | Permite al cliente elegir un horario realmente reservable. |
| Estimable | No | Faltan anticipación máxima, zona horaria y respuesta cuando no hay horarios. |
| Pequeña | Sí | Cubre la consulta semanal y selección inicial. |
| Testeable | Sí | Los slots pueden contrastarse con reglas, reservas y bloqueos preparados. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Consultar una semana con horarios disponibles

**Given** que el profesional tiene disponibilidad vigente
**When** el cliente abre una semana de su calendario público
**Then** el sistema muestra los horarios futuros que no estén reservados ni bloqueados
**And** permite seleccionar uno para iniciar la reserva

### Escenario 2: Excluir horarios no reservables

**Given** que una franja contiene horarios pasados, confirmados o bloqueados
**When** el cliente consulta la semana
**Then** el sistema no ofrece esos horarios como seleccionables

### Escenario 3: Semana sin disponibilidad

**Given** que ningún horario de la semana cumple las reglas de disponibilidad
**When** el cliente consulta esa semana
**Then** el sistema no presenta horarios seleccionables

## Notas de QA

* Preparar slots pasados, confirmados, cancelados y bloqueados.
* Verificar límites de día y semana en la zona horaria finalmente acordada.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-16.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Vista semanal y selección de horario | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 5.1 |
| Exclusión de pasado | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-03 |
| Cálculo mediante reglas, turnos y bloqueos | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Los slots |

## Contradicciones detectadas

* La documentación describe el cálculo de slots, pero no define una zona horaria de negocio; no se deduce una a partir del entorno observado.

## Preguntas abiertas

* ¿Qué zona horaria determina fechas, semanas y horarios visibles?
* ¿Existe anticipación máxima o mínima para reservar?
* ¿Qué mensaje se muestra cuando una semana no tiene horarios?
