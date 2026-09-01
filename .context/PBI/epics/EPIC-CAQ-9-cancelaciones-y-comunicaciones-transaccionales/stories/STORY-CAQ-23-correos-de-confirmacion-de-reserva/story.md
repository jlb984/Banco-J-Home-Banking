# Story: Como participante de una reserva, quiero recibir su confirmación por correo, para conservar los datos del turno

**ID:** CAQ-23
**Epic:** CAQ-9
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como participante de una reserva, quiero recibir su confirmación por correo, para conservar los datos del turno.

## Criterios de Aceptación (Borrador)

- [ ] Al confirmar una reserva, el cliente recibe un correo con el detalle del turno.
- [ ] El correo del cliente incluye el enlace único de cancelación.
- [ ] El profesional recibe un aviso de nueva reserva.
- [ ] Los correos de producto se envían mediante Resend.
- [ ] La reserva no se informa como fallida si el turno fue creado pero el correo no pudo entregarse.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Destinatarios, detalle y enlace de cancelación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 7 |
| Proveedor vigente Resend | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · resumen del 03/03/2026 |
| Independencia entre creación y entrega | **Hipótesis** — las notas técnicas documentan envío sincrónico, pero no existe una regla acordada para fallas parciales |
