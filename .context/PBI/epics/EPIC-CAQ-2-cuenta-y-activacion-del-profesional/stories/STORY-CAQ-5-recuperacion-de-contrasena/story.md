# Story: Recuperación de contraseña del profesional

**ID:** CAQ-5
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero solicitar un enlace de recuperación mediante mi correo electrónico y establecer una nueva contraseña, para volver a acceder sin revelar si mi correo está registrado.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede validarse con cuentas existentes y no existentes sin depender de las funciones de agenda o reservas. |
| Negociable | Sí | El objetivo de recuperación segura y no enumerativa está definido; la presentación y los controles adicionales siguen siendo negociables. |
| Valiosa | Sí | Permite recuperar el acceso sin intervención manual y protege la existencia de las cuentas. |
| Estimable | No | Faltan decisiones sobre la política de la nueva contraseña, los mensajes para enlaces inválidos y los límites de solicitudes repetidas. |
| Pequeña | Sí | Comprende un único flujo de recuperación compuesto por solicitud, recepción del enlace y cambio de contraseña. |
| Testeable | Sí | La respuesta no enumerativa, la vigencia de una hora, el uso único y el cambio de contraseña pueden comprobarse con buzones y cuentas de prueba. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Solicitud para un correo registrado

**Given** que existe una cuenta profesional asociada al correo informado

**When** el profesional solicita recuperar su contraseña

**Then** el sistema muestra el mensaje «Si el email existe en nuestro sistema, recibirás un enlace para recuperar tu contraseña»

**And** envía al correo registrado un enlace con un token de un solo uso

### Escenario 2: Solicitud para un correo no registrado

**Given** que no existe una cuenta asociada al correo informado

**When** el usuario solicita recuperar la contraseña

**Then** el sistema muestra el mensaje «Si el email existe en nuestro sistema, recibirás un enlace para recuperar tu contraseña»

**And** la respuesta visible no revela que el correo no está registrado

### Escenario 3: Solicitud sin un correo válido

**Given** que el usuario deja vacío el correo o informa un valor con formato inválido

**When** intenta solicitar la recuperación

**Then** el sistema no procesa la solicitud

**And** solicita que se informe un correo electrónico válido

### Escenario 4: Cambio de contraseña con un token vigente

**Given** que el profesional abre un enlace de recuperación no utilizado antes de que transcurra una hora desde su emisión

**When** establece una nueva contraseña

**Then** el sistema actualiza la contraseña de la cuenta

**And** permite recuperar el acceso con la nueva contraseña

### Escenario 5: Intento con un token vencido

**Given** que transcurrió una hora o más desde la emisión del token de recuperación

**When** el profesional intenta utilizar el enlace

**Then** el sistema rechaza el cambio de contraseña

**And** no modifica la contraseña de la cuenta

### Escenario 6: Reutilización de un token

**Given** que el token de recuperación ya fue utilizado para cambiar la contraseña

**When** se intenta utilizar nuevamente el mismo enlace

**Then** el sistema rechaza el cambio de contraseña

**And** no modifica la contraseña de la cuenta

## Notas de QA

* Usar una cuenta existente y un correo no registrado bajo control del equipo; comparar que ambos casos presenten exactamente el mismo mensaje visible.
* Verificar los límites temporales inmediatamente antes y a partir de una hora desde la emisión, utilizando control del reloj o tokens preparados en un entorno de prueba.
* Comprobar el uso único intentando abrir el mismo enlace después de un cambio exitoso.
* Verificar que el correo de recuperación pertenece al flujo de autenticación gestionado por Supabase y no a los correos de producto enviados mediante Resend.
* No utilizar cuentas, correos ni credenciales reales; el único entorno documentado es producción y este refinamiento no autoriza generar correos ni modificar contraseñas allí.
* La implementación continúa `Sin verificar`; el uso de PKCE y la vigencia documentada no prueban el comportamiento actual.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-5.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| La recuperación se solicita mediante el correo electrónico | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.3 |
| La respuesta visible es idéntica exista o no la cuenta | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.3; `.context/architecture/prd.md` · Feature 1 y Requisitos No Funcionales |
| Mensaje «Si el email existe en nuestro sistema, recibirás un enlace para recuperar tu contraseña» | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.3 |
| El enlace contiene un token de un solo uso que vence a la hora | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.3; `.context/Confluence-corporativo/04-notas-tecnicas.md` · Auth |
| El flujo de cambio de contraseña utiliza PKCE | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Auth |
| Los correos de recuperación pertenecen a autenticación y permanecen en Supabase | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · correo del 28/02/2026 |
| Rechazar una solicitud cuando el correo está vacío o tiene formato inválido | **Hipótesis** — no hay documento que defina la validación ni su mensaje para este formulario |

## Contradicciones detectadas

* Ninguna detectada. La decisión posterior de mantener los correos de autenticación en Supabase es compatible con la especificación funcional del enlace de recuperación.

## Preguntas abiertas

* ¿Qué reglas debe cumplir la nueva contraseña y son exactamente las mismas que se aplican durante el registro?
* ¿Qué mensajes deben mostrarse cuando el correo está vacío o tiene formato inválido, y cuando el token está vencido, ya fue utilizado o es inválido?
* ¿Una nueva solicitud invalida los enlaces de recuperación emitidos anteriormente para la misma cuenta?
* ¿Existe un límite de solicitudes por correo, dirección IP o período? En caso afirmativo, ¿cuál es el comportamiento al alcanzarlo?
* ¿Después del cambio exitoso se inicia sesión automáticamente o el profesional debe volver al login?
