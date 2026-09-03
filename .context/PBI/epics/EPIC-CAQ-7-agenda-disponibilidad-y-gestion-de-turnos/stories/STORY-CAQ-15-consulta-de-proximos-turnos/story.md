# Story: Como profesional, quiero consultar mis próximos turnos, para organizar mi jornada

**ID:** CAQ-15
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero consultar mis próximos turnos, para organizar mi jornada.

## Criterios de Aceptación (Borrador)

- [ ] Un profesional autenticado puede consultar los turnos asociados con su cuenta.
- [ ] La agenda presenta los turnos próximos.
- [ ] Cada turno permite distinguir su horario y estado.
- [ ] La consulta no expone turnos pertenecientes a otro profesional.
- [ ] Los estados documentados son `confirmed` y `cancelled`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Consulta de agenda y próximos turnos | `.context/architecture/prd.md` · Feature 2; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.1 |
| Aislamiento por profesional | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Row level security y endpoints |
| Estados de turno | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 9 |
| Presentación exacta de horario y estado | **Hipótesis** — son datos mínimos para identificar un turno, pero la documentación no define el diseño de la agenda |

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
