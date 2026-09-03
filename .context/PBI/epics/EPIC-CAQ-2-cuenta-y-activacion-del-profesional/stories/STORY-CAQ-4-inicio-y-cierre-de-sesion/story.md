# Story: Inicio y cierre de sesión del profesional

**ID:** CAQ-4
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero iniciar sesión con mi correo electrónico y contraseña y cerrar la sesión cuando termine, para acceder a mi panel y proteger la información de mi cuenta.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede validarse con una cuenta profesional existente, sin depender de las funciones de agenda o reservas. |
| Negociable | Sí | El objetivo de acceso seguro está definido; la navegación y la presentación de errores siguen siendo negociables. |
| Valiosa | Sí | Permite al profesional acceder a su panel y finalizar el acceso cuando deja de utilizarlo. |
| Estimable | No | No está acordado qué debe ocurrir con la navegación, el contenido visible y las rutas protegidas después del logout. |
| Pequeña | No | Reúne inicio de sesión, cierre de sesión y protección de rutas. Si la incertidumbre impide completarla, dividir en acceso autenticado y revocación de acceso. |
| Testeable | No | El login y el mensaje genérico son verificables, pero no puede emitirse un veredicto sobre los escenarios posteriores al logout hasta confirmar su resultado esperado. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Inicio de sesión exitoso

**Given** que existe una cuenta profesional y el usuario no tiene una sesión activa

**When** informa el correo electrónico y la contraseña correctos

**Then** el sistema inicia la sesión

**And** permite acceder al dashboard del profesional

### Escenario 2: Intento con un correo incorrecto

**Given** que el profesional no tiene una sesión activa

**When** intenta iniciar sesión con un correo electrónico incorrecto

**Then** el sistema rechaza el acceso con el mensaje «Email o contraseña incorrectos»

**And** no indica cuál de las credenciales falló

### Escenario 3: Intento con una contraseña incorrecta

**Given** que el profesional no tiene una sesión activa

**When** intenta iniciar sesión con una contraseña incorrecta

**Then** el sistema rechaza el acceso con el mensaje «Email o contraseña incorrectos»

**And** no indica cuál de las credenciales falló

### Escenario 4: Intento sin una de las credenciales

**Given** que el profesional deja vacío el correo electrónico o la contraseña

**When** intenta iniciar sesión

**Then** el sistema no inicia la sesión

**And** no permite acceder al dashboard

### Escenario 5: Acceso al dashboard con una sesión válida

**Given** que el profesional tiene una sesión válida

**When** abre una ruta protegida del dashboard

**Then** el sistema muestra únicamente el contenido correspondiente a su cuenta

### Escenario 6: Cierre de una sesión activa

**Given** que el profesional tiene una sesión activa

**When** selecciona la opción «Salir»

**Then** el sistema finaliza la sesión

**And** la navegación deja de presentar las opciones exclusivas de una sesión activa

### Escenario 7: Acceso directo al dashboard sin sesión

**Given** que el profesional no tiene una sesión activa

**When** intenta abrir directamente una ruta protegida del dashboard

**Then** el sistema impide el acceso

**And** no expone contenido correspondiente a la cuenta profesional

### Escenario 8: Reingreso a una ruta protegida después del logout

**Given** que el profesional cerró su sesión

**When** vuelve a abrir una ruta protegida del dashboard

**Then** el sistema impide el acceso

**And** no expone contenido correspondiente a la sesión finalizada

## Notas de QA

* Ejecutar los intentos con correo incorrecto y contraseña incorrecta por separado para comprobar que ambos devuelven el mismo mensaje genérico.
* Verificar el acceso directo a `/dashboard`, `/dashboard/availability` y `/dashboard/clients` con sesión válida, sin sesión y después del logout.
* Comprobar el cierre de sesión en la pestaña actual y el efecto sobre otras pestañas abiertas, sin asumir el resultado hasta que producto responda la pregunta abierta.
* No usar credenciales ni información personal reales; el único entorno documentado es producción y no está autorizado modificar datos durante este refinamiento.
* La implementación continúa `Sin verificar`; los datos observados documentan una brecha, pero este refinamiento no comprueba que siga vigente.

## Inspección Shift-Left

**Resultado:** Bloqueante

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-4.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| El inicio de sesión utiliza correo electrónico y contraseña | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.2 |
| Las credenciales incorrectas producen el mensaje «Email o contraseña incorrectos» sin revelar cuál falló | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.2 |
| La autenticación utiliza Supabase Auth, cookies `httpOnly` y middleware para proteger el dashboard | `.context/Confluence-corporativo/04-notas-tecnicas.md` · sección Auth; `.context/architecture/prd.md` · Requisitos No Funcionales |
| Una sesión válida permitió iniciar sesión y acceder a `/dashboard` | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Feature 1 y Fuentes |
| «Salir» cambió la navegación a las opciones de usuario no autenticado | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Seguridad observada |
| Después del logout, `/dashboard`, `/dashboard/availability` y `/dashboard/clients` continuaron renderizando sus pantallas | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Seguridad observada y Fuentes |
| Sin sesión o después del logout, las rutas protegidas deben impedir el acceso y no exponer contenido de la cuenta | **Hipótesis** — el dashboard está documentado como protegido, pero no existe una decisión funcional explícita sobre el resultado posterior al logout |

## Contradicciones detectadas

* La especificación y las notas técnicas presentan el dashboard como protegido por sesión y middleware; la observación de producción del 30/08/2026 registró que tres rutas continuaron renderizando sus pantallas después del logout. No se determinó si se trató de contenido residual, caché o autorización incompleta. Se conserva la protección como comportamiento esperado bajo hipótesis y la implementación permanece `Sin verificar`.

## Preguntas abiertas

* ¿Después del logout el sistema debe redirigir inmediatamente al login, mostrar otra pantalla o permanecer en la ruta actual sin contenido privado?
* ¿Qué contenido debe eliminarse inmediatamente de la interfaz y de la caché del navegador al cerrar sesión?
* ¿El logout debe invalidar simultáneamente la sesión en todas las pestañas y dispositivos o únicamente en el contexto actual?
* ¿Qué mensaje debe mostrarse cuando falta el correo electrónico o la contraseña?
* ¿Debe bloquearse temporalmente una cuenta después de varios intentos fallidos? En caso afirmativo, ¿después de cuántos intentos y durante cuánto tiempo?
