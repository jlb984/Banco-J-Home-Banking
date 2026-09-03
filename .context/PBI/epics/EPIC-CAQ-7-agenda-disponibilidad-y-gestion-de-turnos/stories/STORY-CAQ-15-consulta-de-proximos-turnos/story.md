# Story: Consulta de próximos turnos

**ID:** CAQ-15
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero consultar mis próximos turnos, para organizar mi jornada.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede validarse con turnos preparados para una cuenta. |
| Negociable | Sí | La consulta está definida; orden, filtros y detalle siguen abiertos. |
| Valiosa | Sí | Permite organizar la jornada del profesional. |
| Estimable | No | Faltan datos mínimos, orden y tratamiento de cancelados. |
| Pequeña | Sí | Se limita a consultar los próximos turnos. |
| Testeable | No | El estado vacío fue observado, pero la lista poblada y su autorización siguen sin verificar. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Consultar próximos turnos propios

**Given** que el profesional tiene una sesión válida y turnos futuros asociados
**When** abre su dashboard
**Then** el sistema presenta únicamente sus próximos turnos
**And** permite distinguir el horario y el estado `confirmed` o `cancelled` de cada uno

### Escenario 2: Mostrar el estado vacío

**Given** que no existen citas próximas visibles para la cuenta
**When** se abre el dashboard
**Then** el sistema muestra «No tienes citas próximas»
**And** muestra «Comparte tu perfil público para empezar a recibir reservas.»

### Escenario 3: Impedir exposición entre profesionales

**Given** que un turno pertenece a otro profesional
**When** el profesional autenticado consulta su agenda
**Then** el sistema no incluye ese turno en la respuesta ni en la interfaz

## Notas de QA

* Preparar turnos pasados, futuros, confirmados y cancelados para dos profesionales.
* El estado vacío está observado; la lista poblada y el aislamiento no lo están.
* La implementación continúa `Sin verificar`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Consulta de agenda y próximos turnos | `.context/architecture/prd.md` · Feature 2; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.1 |
| Aislamiento por profesional | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Row level security y endpoints |
| Estados de turno | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 9 |
| Presentación exacta de horario y estado | **Hipótesis** — son datos mínimos para identificar un turno, pero la documentación no define el diseño de la agenda |
| Textos del estado vacío | **Observado** — producción, 02/09/2026. Evidencia: `evidence/2026-09-02-dashboard-sin-citas.png` |

## Comportamiento observado

| Qué hace | Evidencia | Qué decía la documentación |
| :--- | :--- | :--- |
| La ruta `/dashboard` renderiza el panel con los indicadores `Citas Hoy`, `Próxima Cita` y la sección `Próximas Citas`. | `evidence/2026-09-02-dashboard-sin-citas.png` | El PRD describe una agenda y consulta de turnos próximos (`.context/architecture/prd.md` · Feature 2), pero no define este estado visual. |
| Cuando no hay citas próximas, se muestra `No tienes citas próximas` y `Comparte tu perfil público para empezar a recibir reservas.` | `evidence/2026-09-02-dashboard-sin-citas.png` | **Nada: ningún documento describe el estado vacío.** |
| No se pudo observar una lista con turnos, sus horarios o estados porque la cuenta disponible no tenía citas y no se crearon datos en producción. | `evidence/2026-09-02-dashboard-sin-citas.png` | La historia exige distinguir horario y estado; queda sin verificar. |

## Contradicciones detectadas

- La ruta `/dashboard` renderizó el estado vacío sin una sesión autenticada visible; esto no permite confirmar el aislamiento por profesional descrito en las fuentes técnicas. El alcance de autorización de datos no se probó.

## Preguntas abiertas

- ¿Qué columnas o datos muestra cada turno cuando existen citas próximas?
- ¿Cómo se ordenan, filtran o agrupan los turnos?
- ¿La lista de turnos requiere autenticación efectiva y cómo se impide consultar la agenda de otro profesional?
