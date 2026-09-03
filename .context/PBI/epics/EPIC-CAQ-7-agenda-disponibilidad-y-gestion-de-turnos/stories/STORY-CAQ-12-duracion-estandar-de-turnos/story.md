# Story: Duración estándar de los turnos

**ID:** CAQ-12
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero definir la duración estándar de mis turnos, para generar horarios acordes con mi servicio.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede validarse sobre una disponibilidad ya configurada. |
| Negociable | Sí | El objetivo está definido; el conjunto de valores sigue abierto. |
| Valiosa | Sí | Permite adecuar los horarios ofrecidos al servicio. |
| Estimable | No | Falta decidir si se admite cualquier entero positivo o solo opciones cerradas. |
| Pequeña | Sí | Modifica una única regla global del profesional. |
| Testeable | No | El cálculo es comprobable, pero el dominio de entrada no está acordado. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Aplicar una duración válida

**Given** que el profesional tiene bloques de disponibilidad configurados
**And** selecciona una duración admitida mayor que cero
**When** guarda la duración estándar
**Then** el sistema aplica esa duración a todos sus turnos
**And** divide cada bloque en horarios consecutivos con esa duración

### Escenario 2: Rechazar una duración no positiva

**Given** que el profesional informa una duración igual o menor que cero
**When** intenta guardar
**Then** el sistema rechaza el valor
**And** conserva la duración anterior

### Escenario 3: No ofrecer un remanente incompleto

**Given** que la duración vigente no divide exactamente un bloque disponible
**When** el sistema calcula sus horarios
**Then** ofrece únicamente turnos completos dentro del bloque

## Notas de QA

* Probar cada opción observada y bloques con división exacta e inexacta.
* No aprobar valores fuera de la interfaz hasta resolver la contradicción.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Bloqueante

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-12.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Duración positiva, única y usada para dividir la franja | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.2 |
| Opciones observadas de 15 a 120 minutos | `.context/architecture/prd.md` · Feature 2 |
| Conjunto definitivo de duraciones permitidas | **Hipótesis** — la especificación admite cualquier entero y la UI observada presenta opciones cerradas |
| Un remanente menor que la duración no genera un horario | **Hipótesis** — no hay documento que defina el redondeo |

## Contradicciones detectadas

* La especificación admite cualquier entero positivo; la interfaz observada ofrece 15, 30, 45, 60, 90 y 120 minutos. No se adopta una de las dos reglas sin decisión de Producto.

## Preguntas abiertas

* ¿La duración válida es cualquier entero positivo o solo 15, 30, 45, 60, 90 y 120 minutos?
* ¿Qué ocurre con turnos futuros cuando cambia la duración?
* ¿Cómo se trata el remanente de un bloque que no alcanza para otro turno completo?
