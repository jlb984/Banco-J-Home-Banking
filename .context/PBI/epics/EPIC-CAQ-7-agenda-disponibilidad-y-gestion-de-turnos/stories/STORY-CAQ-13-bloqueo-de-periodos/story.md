# Story: Como profesional, quiero bloquear períodos puntuales, para evitar reservas cuando no estoy disponible

**ID:** CAQ-13
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero bloquear períodos puntuales, para evitar reservas cuando no estoy disponible.

## Criterios de Aceptación (Borrador)

- [ ] El profesional puede indicar fecha y hora de inicio y de fin del bloqueo.
- [ ] El profesional puede informar un motivo opcional.
- [ ] Los horarios incluidos en el bloqueo dejan de ofrecerse para nuevas reservas.
- [ ] El profesional puede consultar y eliminar sus bloqueos.
- [ ] El sistema no cancela ni altera silenciosamente turnos existentes dentro del período mientras la regla de negocio permanezca abierta.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Rango, motivo opcional y exclusión de horarios | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.3 |
| Consulta, creación y eliminación de bloqueos | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Endpoints |
| Tratamiento de turnos existentes | **Hipótesis de seguridad funcional** — la documentación mantiene abierta la regla y soporte confirma que actualmente permanecen confirmados |
