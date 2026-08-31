# Story: Inicio de sesión
**ID:** PBI-03
**Epic:** PBI-01
**Implementación:** Sin verificar
**Estado de sincronización:** PENDIENTE DE SUBIR A JIRA

## Descripción
Como profesional independiente, quiero iniciar sesión con mi correo y contraseña, para acceder a la configuración de mi agenda y ver mis turnos.

## Criterios de Aceptación (Borrador)
- [ ] El sistema debe permitir ingresar con correo electrónico y contraseña registrados.
- [ ] Ante credenciales incorrectas, el mensaje debe ser genérico: "Email o contraseña incorrectos".
- [ ] Al cerrar sesión, las rutas del dashboard no deben permitir visualizar datos ni interactuar sin reautenticarse.

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Reglas de acceso y mensaje genérico de error | `03-especificacion-funcional-v0.3.md` · sección 3.2 |
| Pantallas del dashboard siguen renderizando tras logout | **Observado** — producción, 30/08/2026. Evidencia: `prd.md` · sección 5 |
