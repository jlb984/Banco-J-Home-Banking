# Story: Como profesional, quiero cargar un cliente manualmente, para mantener completo mi registro

**ID:** CAQ-26
**Epic:** CAQ-10
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero cargar un cliente manualmente, para mantener completo mi registro.

## Criterios de Aceptación (Borrador)

- [ ] El profesional puede iniciar el alta manual desde su panel de clientes.
- [ ] El alta registra nombre y correo electrónico.
- [ ] El correo se utiliza para determinar si el cliente ya existe.
- [ ] Si es un cliente nuevo y el profesional ya alcanzó diez clientes únicos, el alta se rechaza.
- [ ] Ante un alta válida, el cliente aparece en el listado del profesional.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Carga manual desde el panel | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.1 |
| Nombre, correo y unicidad | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Tablas |
| Aplicación del límite al alta manual | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 8.1 y 8.2 |
| Aparición inmediata en el listado | **Hipótesis** — es el resultado esperado del alta, pero la documentación no define la actualización de la interfaz |
