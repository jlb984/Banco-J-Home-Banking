# Story: Como cliente final, quiero cancelar mediante el enlace de mi correo, para liberar el horario sin crear una cuenta

**ID:** CAQ-20
**Epic:** CAQ-9
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como cliente final, quiero cancelar mediante el enlace de mi correo, para liberar el horario sin crear una cuenta.

## Criterios de Aceptación (Borrador)

- [ ] El correo de confirmación incluye un enlace único de cancelación.
- [ ] El enlace permite cancelar sin iniciar sesión.
- [ ] Solo se puede cancelar un turno que no esté en el pasado.
- [ ] La cancelación cambia el estado del turno a `cancelled`.
- [ ] El horario cancelado vuelve a estar disponible.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Enlace único sin cuenta | `.context/Confluence-corporativo/01-minuta-kickoff.md` · Los dos usuarios del sistema; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.1 |
| Restricción temporal, estado y liberación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.3 |
| Riesgo del endpoint público | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Endpoints |
