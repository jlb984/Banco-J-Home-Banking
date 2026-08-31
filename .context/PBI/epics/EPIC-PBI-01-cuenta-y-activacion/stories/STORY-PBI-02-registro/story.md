# Story: Registro de cuenta y generación de URL
**ID:** PBI-02
**Epic:** PBI-01
**Implementación:** Sin verificar
**Estado de sincronización:** PENDIENTE DE SUBIR A JIRA

## Descripción
Como profesional independiente, quiero registrarme indicando mi nombre, correo y contraseña, para obtener una cuenta y una URL pública donde recibir reservas.

## Criterios de Aceptación (Borrador)
- [ ] El sistema debe requerir nombre completo, email (con formato válido y no registrado) y contraseña (mín. 8 caracteres, 1 mayúscula, 1 número).
- [ ] Al registrarse con éxito, el sistema debe iniciar sesión automáticamente.
- [ ] El sistema debe generar una URL pública única a partir del nombre, agregando sufijos numéricos en caso de colisión.
- [ ] El sistema debe enviar un correo electrónico de bienvenida.
- [ ] En caso de email ya registrado, se debe mostrar "El email ya está en uso" con un enlace a recuperación.

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Validaciones, inicio de sesión y URL pública | `03-especificacion-funcional-v0.3.md` · sección 3.1 |
| Mecanismo de generación de URL incremental | `03-especificacion-funcional-v0.3.md` · sección 3.4 |
| Ausencia de URL pública en la navegación de la UI | **Observado** — producción, 30/08/2026. Evidencia: `prd.md` · sección 4 |
