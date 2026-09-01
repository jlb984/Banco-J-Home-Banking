# Story: Como profesional, quiero iniciar y cerrar sesión, para acceder de forma segura a mi panel

**ID:** CAQ-4
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero iniciar y cerrar sesión, para acceder de forma segura a mi panel.

## Criterios de Aceptación (Borrador)

- [ ] El profesional puede iniciar sesión mediante correo electrónico y contraseña.
- [ ] Ante credenciales incorrectas, el sistema muestra un mensaje genérico que no revela cuál de los datos falló.
- [ ] Una sesión válida permite acceder a las rutas protegidas del dashboard.
- [ ] Al cerrar sesión, las rutas protegidas dejan de exponer el contenido del profesional.
- [ ] El comportamiento de redirección y limpieza de contenido posterior al logout debe definirse antes de considerar cerrado este criterio.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Inicio de sesión mediante correo y contraseña | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.2 |
| Mensaje no enumerativo ante credenciales incorrectas | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.2 |
| Dashboard protegido por sesión y middleware | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Auth y endpoints |
| Las rutas protegidas no deben exponer contenido tras el logout | **Hipótesis** — el PRD registra el comportamiento observado como riesgo y pregunta abierta, pero no existe una decisión funcional explícita |
| Redirección y limpieza del contenido al cerrar sesión | **Hipótesis** — `.context/architecture/prd.md` · Preguntas abiertas |
