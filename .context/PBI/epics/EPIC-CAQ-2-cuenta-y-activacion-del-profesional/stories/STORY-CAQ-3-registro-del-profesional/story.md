# Story: Registro del profesional

**ID:** CAQ-3
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero registrarme con mi nombre completo, correo electrónico y contraseña, para crear mi cuenta, iniciar sesión y comenzar a configurar mi agenda.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede desarrollarse y validarse como puerta de entrada al producto, aunque necesita los servicios de autenticación, generación de URL y correo. |
| Negociable | Sí | El valor y las reglas están definidos; la solución técnica y la presentación de las validaciones siguen siendo negociables. |
| Valiosa | Sí | Permite que el profesional cree su cuenta y comience la activación necesaria para recibir reservas. |
| Estimable | Sí | Los campos, límites, reglas y resultados esperados están documentados; las preguntas abiertas afectan detalles de validación y fallos parciales, no impiden una estimación inicial. |
| Pequeña | No | Incluye cinco resultados observables: crear la cuenta, iniciar sesión, generar la URL, redirigir y enviar el correo. Si no cabe en una iteración, dividir en registro y sesión, generación de URL y bienvenida, conservando esta historia como flujo integrador. |
| Testeable | Sí | Las entradas, los límites y los efectos del registro pueden comprobarse; la política real aplicada por autenticación permanece sin verificar. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Registro exitoso del profesional

**Given** que el correo electrónico no está registrado y el profesional informa un nombre completo de hasta 100 caracteres, un correo válido de hasta 254 caracteres y una contraseña de al menos 8 caracteres con una mayúscula y un número

**When** envía el formulario de registro

**Then** el sistema crea la cuenta e inicia la sesión automáticamente

**And** genera una URL pública única para el profesional

**And** redirige al asistente de configuración inicial

**And** envía el correo de bienvenida al profesional

### Escenario 2: Rechazo de campos obligatorios vacíos

**Given** que el profesional deja vacío el nombre completo, el correo electrónico o la contraseña

**When** intenta enviar el formulario de registro

**Then** el sistema rechaza el registro

**And** no crea la cuenta

### Escenario 3: Rechazo de un nombre que supera el máximo

**Given** que el profesional informa un nombre completo de más de 100 caracteres

**When** intenta registrarse

**Then** el sistema rechaza el registro

**And** no crea la cuenta

### Escenario 4: Rechazo de un correo con formato inválido

**Given** que el profesional informa un correo electrónico con formato inválido

**When** intenta registrarse

**Then** el sistema rechaza el registro

**And** no crea la cuenta

### Escenario 5: Rechazo de un correo que supera el máximo

**Given** que el profesional informa un correo electrónico de más de 254 caracteres

**When** intenta registrarse

**Then** el sistema rechaza el registro

**And** no crea la cuenta

### Escenario 6: Rechazo de un correo ya registrado

**Given** que ya existe una cuenta con el correo electrónico informado

**When** el profesional intenta registrarse con ese correo

**Then** el sistema rechaza el registro con el mensaje «El email ya está en uso»

**And** ofrece un enlace a la recuperación de contraseña

**And** no crea una segunda cuenta

### Escenario 7: Rechazo de una contraseña demasiado corta

**Given** que el profesional informa una contraseña de menos de 8 caracteres

**When** intenta registrarse

**Then** el sistema rechaza el registro con el mensaje «La contraseña es muy corta»

**And** no crea la cuenta

### Escenario 8: Rechazo de una contraseña sin mayúscula

**Given** que el profesional informa una contraseña de al menos 8 caracteres y con un número, pero sin ninguna letra mayúscula

**When** intenta registrarse

**Then** el sistema rechaza el registro

**And** no crea la cuenta

### Escenario 9: Rechazo de una contraseña sin número

**Given** que el profesional informa una contraseña de al menos 8 caracteres y con una letra mayúscula, pero sin ningún número

**When** intenta registrarse

**Then** el sistema rechaza el registro

**And** no crea la cuenta

### Escenario 10: Generación de una URL única ante nombres coincidentes

**Given** que ya existe en la plataforma una URL pública generada a partir del mismo nombre completo

**When** se completa el registro del nuevo profesional

**Then** el sistema agrega a la URL un sufijo numérico incremental que no esté utilizado

**And** la URL resultante es única en toda la plataforma

## Notas de QA

* Probar los límites de nombre con 100 y 101 caracteres, y los de correo con 254 y 255 caracteres.
* Cubrir contraseñas de 7 y 8 caracteres, con y sin mayúscula, y con y sin número.
* Usar cuentas y correos sintéticos en un entorno habilitado para pruebas; no crear datos ni enviar correos desde producción sin autorización.
* Verificar por separado los cinco efectos del flujo exitoso: cuenta, sesión, URL, redirección y correo.
* La implementación continúa `Sin verificar`; este refinamiento no confirma el comportamiento de la interfaz ni de Supabase.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| El profesional se registra con nombre, correo electrónico y contraseña | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 2.1 y 3.1 |
| Nombre obligatorio, no vacío y de hasta 100 caracteres | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| Correo obligatorio, válido, de hasta 254 caracteres y no registrado previamente | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| Contraseña obligatoria de al menos 8 caracteres, con una mayúscula y un número | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| Mensajes «El email ya está en uso» y «La contraseña es muy corta» | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| El correo duplicado ofrece un enlace a recuperación de contraseña | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.1 |
| El registro crea la cuenta y la sesión, genera la URL, redirige a la configuración y envía la bienvenida | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 3.1 y 7; `.context/architecture/prd.md` · Feature 1 y User Journeys |
| La URL se normaliza desde el nombre y resuelve colisiones con un sufijo numérico incremental | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.4 |
| Los correos de producto se envían mediante Resend | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · resumen del 03/03/2026 y correo del 28/02/2026 |

## Contradicciones detectadas

* La especificación exige una contraseña de al menos 8 caracteres, con una mayúscula y un número; `.context/PBI/epic-tree.md` y `.context/architecture/prd.md` indican que no existe evidencia actual de que la interfaz y Supabase apliquen exactamente esas reglas. Se conserva la especificación como comportamiento esperado y la implementación permanece `Sin verificar`.

## Preguntas abiertas

* ¿Qué mensajes deben mostrarse cuando falta un campo, el nombre o correo superan su máximo, el correo tiene formato inválido o la contraseña no contiene una mayúscula o un número?
* ¿Se eliminan espacios al inicio y al final del nombre y del correo antes de validar y guardar?
* ¿Los correos se normalizan para detectar duplicados sin distinguir mayúsculas y minúsculas?
* ¿Qué debe ocurrir y qué debe ver el profesional si se crea la cuenta, pero falla la generación de la URL, la redirección o el envío del correo de bienvenida?
* ¿El registro requiere confirmar el correo electrónico antes de permitir usar la cuenta, o la sesión automática queda habilitada inmediatamente?
