# Story: Como profesional, quiero recuperar mi contraseña, para volver a acceder sin revelar si mi correo está registrado

**ID:** CAQ-5
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero recuperar mi contraseña, para volver a acceder sin revelar si mi correo está registrado.

## Criterios de Aceptación (Borrador)

- [ ] El profesional puede solicitar la recuperación mediante su correo electrónico.
- [ ] La respuesta visible es la misma tanto si el correo existe como si no existe en el sistema.
- [ ] Para una cuenta existente, el sistema envía un enlace con un token de un solo uso.
- [ ] El token de recuperación vence una hora después de su emisión.
- [ ] Un token válido permite establecer una nueva contraseña y recuperar el acceso.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Solicitud de recuperación por correo y respuesta no enumerativa | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.3 |
| Token de un solo uso con vigencia de una hora | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.3 |
| Uso del token para establecer una contraseña nueva | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Auth |
