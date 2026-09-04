# Story: Configuración de disponibilidad semanal

**ID:** BJHB-15
**Epic:** BJHB-3
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)
**Estado:** Refinado

## Descripción

Como profesional, quiero configurar mi disponibilidad semanal, para ofrecer únicamente los horarios en los que atiendo.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede validarse con una cuenta profesional sin crear reservas. |
| Negociable | Sí | La regla semanal está definida; la interacción de edición queda abierta. |
| Valiosa | Sí | Determina cuándo puede recibir reservas el profesional. |
| Estimable | Sí | Están definidos bloques, validaciones y reemplazo de reglas. |
| Pequeña | Sí | Se limita a administrar la disponibilidad recurrente. |
| Testeable | Sí | Las reglas guardadas y los slots resultantes son observables. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Guardar una disponibilidad semanal válida

**Given** que el profesional está autenticado
**And** define uno o más bloques de atención por día
**And** cada hora de fin es posterior a su hora de inicio
**And** los bloques del mismo día no se solapan
**When** guarda la configuración
**Then** el sistema reemplaza las reglas semanales anteriores por las informadas
**And** calcula la disponibilidad pública únicamente con las reglas vigentes

### Escenario 2: Rechazar un bloque con rango inválido

**Given** que un bloque tiene una hora de fin igual o anterior a la hora de inicio
**When** el profesional intenta guardar
**Then** el sistema rechaza la configuración
**And** conserva las reglas anteriores

### Escenario 3: Rechazar bloques solapados

**Given** que dos bloques del mismo día se superponen
**When** el profesional intenta guardar
**Then** el sistema rechaza la configuración
**And** conserva las reglas anteriores

## Notas de QA

* Probar días sin atención, varios bloques válidos y límites contiguos.
* Comprobar el reemplazo completo y su efecto en el endpoint público.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-BJHB-15.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Configuración por día y validaciones de los bloques | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.1 |
| Reemplazo completo al guardar | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.1; `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · Horarios |
| Uso de las reglas para calcular slots | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Los slots |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué zona horaria se usa para guardar y presentar los bloques?
* ¿Se permiten bloques contiguos y bloques que crucen la medianoche?
* ¿Qué mensaje debe mostrarse para cada validación fallida?
