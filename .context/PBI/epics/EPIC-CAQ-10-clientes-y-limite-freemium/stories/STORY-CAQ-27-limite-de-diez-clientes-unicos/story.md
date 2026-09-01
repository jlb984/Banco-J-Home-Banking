# Story: Como responsable del producto, quiero limitar el plan gratuito a diez clientes únicos, para validar la intención de conversión

**ID:** CAQ-27
**Epic:** CAQ-10
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como responsable del producto, quiero limitar el plan gratuito a diez clientes únicos, para validar la intención de conversión.

## Criterios de Aceptación (Borrador)

- [ ] El límite se calcula por profesional sobre clientes distintos identificados por correo electrónico.
- [ ] Los clientes existentes pueden continuar reservando sin límite de cantidad de turnos.
- [ ] La reserva del cliente nuevo número once se rechaza.
- [ ] La carga manual de un cliente nuevo también se rechaza al alcanzar el límite.
- [ ] El cliente bloqueado recibe un mensaje que le indica contactar directamente al profesional.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Límite, unicidad por correo y continuidad de clientes existentes | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.1 |
| Bloqueo de reserva y alta manual | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.2 |
| Mensaje al cliente nuevo bloqueado | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.2 |
