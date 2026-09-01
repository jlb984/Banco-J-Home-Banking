# Story: Como parte de un turno cancelado, quiero recibir un aviso, para conocer el cambio

**ID:** CAQ-22
**Epic:** CAQ-9
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como parte de un turno cancelado, quiero recibir un aviso, para conocer el cambio.

## Criterios de Aceptación (Borrador)

- [ ] Cuando cancela el cliente, el sistema envía un aviso al profesional.
- [ ] Cuando cancela el profesional, el sistema envía un aviso al cliente.
- [ ] El aviso identifica quién canceló.
- [ ] No se envía el aviso de cancelación a la misma parte que inició la acción.
- [ ] Una falla de entrega no debe revertir silenciosamente el estado ya cancelado del turno.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Destinatario y contenido del aviso | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 6.3 y 7 |
| Existencia actual del correo de cancelación | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · correo del 28/02/2026 |
| Manejo de una falla de correo posterior a cancelar | **Hipótesis** — la documentación indica envíos sincrónicos, pero no define atomicidad entre estado y notificación |
