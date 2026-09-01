# Story: Como cliente final, quiero acceder a la página pública de un profesional, para identificar con quién voy a reservar

**ID:** CAQ-17
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como cliente final, quiero acceder a la página pública de un profesional, para identificar con quién voy a reservar.

## Criterios de Aceptación (Borrador)

- [ ] La página es accesible sin iniciar sesión mediante la URL pública del profesional.
- [ ] La URL resuelve un slug único en toda la plataforma.
- [ ] La página obtiene únicamente el perfil correspondiente al slug solicitado.
- [ ] Una URL válida permite continuar hacia la consulta de disponibilidad.
- [ ] El dominio vigente es `https://cita-ai.vercel.app/`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Acceso público sin cuenta y por slug | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 2.2 y 3.4 |
| Consulta pública del perfil | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Row level security y endpoints públicos |
| Dominio vigente | `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · La dirección |
| Contenido visual exacto del perfil | **Hipótesis pendiente** — la documentación no enumera los datos visibles en la página |
