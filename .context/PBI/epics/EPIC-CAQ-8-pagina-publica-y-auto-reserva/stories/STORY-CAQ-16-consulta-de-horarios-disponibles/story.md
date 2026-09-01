# Story: Como cliente final, quiero consultar los horarios disponibles, para elegir una opción conveniente

**ID:** CAQ-16
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como cliente final, quiero consultar los horarios disponibles, para elegir una opción conveniente.

## Criterios de Aceptación (Borrador)

- [ ] El cliente puede consultar los horarios disponibles de una semana.
- [ ] No se ofrecen horarios pasados.
- [ ] No se ofrecen horarios ocupados por turnos confirmados.
- [ ] No se ofrecen horarios incluidos en bloqueos del profesional.
- [ ] El calendario permite seleccionar un horario disponible para iniciar la reserva.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Vista semanal y selección de horario | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 5.1 |
| Exclusión de pasado | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-03 |
| Cálculo mediante reglas, turnos y bloqueos | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Los slots |
