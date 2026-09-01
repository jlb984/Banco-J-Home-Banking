# Story: Como profesional, quiero registrarme, para comenzar a configurar mi agenda

**ID:** CAQ-3
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero registrarme, para comenzar a configurar mi agenda.

## Criterios de Aceptación (Borrador)

- [ ] El formulario exige nombre completo, correo electrónico y contraseña.
- [ ] El nombre no puede estar vacío ni superar 100 caracteres, y el correo debe tener formato válido, no superar 254 caracteres y no estar registrado previamente.
- [ ] La contraseña debe tener al menos ocho caracteres, una letra mayúscula y un número.
- [ ] Un registro válido crea la cuenta, inicia la sesión automáticamente y dirige al profesional a la configuración inicial.
- [ ] El registro genera un slug público único y envía un correo de bienvenida.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Campos y validaciones del registro | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| Creación de cuenta, sesión automática y configuración inicial | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| Generación de URL y correo de bienvenida | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 3.1 y 7 |
