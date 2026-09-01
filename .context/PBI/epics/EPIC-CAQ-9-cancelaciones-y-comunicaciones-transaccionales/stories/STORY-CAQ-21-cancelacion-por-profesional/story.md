# Story: Como profesional, quiero cancelar un turno desde mi panel, para actualizar mi agenda

**ID:** CAQ-21
**Epic:** CAQ-9
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero cancelar un turno desde mi panel, para actualizar mi agenda.

## Criterios de Aceptación (Borrador)

- [ ] El profesional autenticado puede iniciar la cancelación desde un turno de su agenda.
- [ ] El profesional solo puede cancelar turnos asociados con su cuenta.
- [ ] No se puede cancelar un turno pasado.
- [ ] La cancelación cambia el estado a `cancelled` y libera el horario.
- [ ] El motivo de cancelación no se exige mientras negocio no defina esa regla.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Cancelación desde el panel | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 2.1 y 6.2 |
| Aislamiento por profesional | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Row level security |
| Restricción temporal, estado y liberación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.3 |
| Motivo de cancelación | **Pregunta abierta** — `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.3 |
