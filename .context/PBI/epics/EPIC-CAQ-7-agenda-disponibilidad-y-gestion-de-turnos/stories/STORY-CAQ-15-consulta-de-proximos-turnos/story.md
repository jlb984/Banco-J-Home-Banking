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
