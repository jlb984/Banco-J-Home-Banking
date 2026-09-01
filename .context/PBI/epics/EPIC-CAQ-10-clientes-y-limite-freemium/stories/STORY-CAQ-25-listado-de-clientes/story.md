# Story: Como profesional, quiero consultar mi listado de clientes, para conocer a las personas que reservaron conmigo

**ID:** CAQ-25
**Epic:** CAQ-10
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero consultar mi listado de clientes, para conocer a las personas que reservaron conmigo.

## Criterios de Aceptación (Borrador)

- [ ] Un profesional autenticado puede consultar los clientes asociados con sus turnos.
- [ ] El listado no expone clientes que nunca reservaron con ese profesional.
- [ ] Cada cliente puede identificarse por nombre y correo electrónico.
- [ ] Un mismo correo se cuenta una sola vez para ese profesional.
- [ ] El historial de turnos por cliente no se considera incluido hasta que exista una definición funcional.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Listado de clientes | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.1 |
| Asociación por turnos y unicidad por correo | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Tablas y límite del plan gratuito |
| Nombre y correo del cliente | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.2 |
| Historial por cliente | **Pregunta abierta** — aparece como necesidad en entrevistas, pero no forma parte del comportamiento especificado |
