# Estrategia de Infraestructura y Entornos: Cita AI

## 1. Tipo de Aplicación y Alcance

- **Plataforma:** aplicación web responsive construida con Next.js; no existe app móvil nativa.
- **Acceso público verificado:** `https://cita-ai.vercel.app/login` muestra login y alterna al registro en la misma ruta.
- **Acceso autenticado verificado:** la cuenta suministrada corresponde a un profesional y permite navegar por Dashboard, Disponibilidad y Clientes.
- **Matriz de compatibilidad:** no hay navegadores, sistemas operativos, versiones, resoluciones ni requisitos de accesibilidad acordados. Cualquier matriz propuesta debe tratarse como hipótesis hasta aprobación.

## 2. Mapa de Entornos (Matriz de URLs)

La nota más reciente declara un único entorno operativo, utilizado por usuarios reales. UAT no se incluye como columna activa porque su existencia y vigencia no están confirmadas.

| Componente | Local | Producción |
| :--- | :--- | :--- |
| **Frontend** | No documentado | `https://cita-ai.vercel.app/` |
| **Backend API** | No documentado | Mismo origen, rutas `/api/*` |
| **Base de Datos/Auth** | No documentado | Proyecto Supabase productivo; identificadores y conexiones restringidos |
| **Correo** | No documentado | Resend para producto y Supabase para autenticación |

### Detalles de Acceso

- **Credenciales de prueba:** no hay usuarios fijos autorizados documentados. Deben referenciarse desde almacenamiento seguro o configuración local ignorada, nunca copiarse al repositorio.
- **Acceso a datos:** no está confirmado para QA. No se debe abrir `.env` ni reutilizar la cuenta de Fernando.
- **Cuenta explorada:** usuario profesional de prueba aportado por el usuario. Su contraseña no se registra en este documento; debe migrarse a un mecanismo seguro si se reutiliza.
- **VPN/Restricciones:** no hay VPN documentada. La restricción principal es operativa: toda escritura conocida afecta producción y puede enviar correos reales.

## 3. Pipeline de CI/CD (Integración Continua)

- **Trigger actual:** push a `main` inicia despliegue automático en Vercel.
- **Validaciones automáticas:** no hay pipeline, tests ni controles previos documentados.
- **Configuración:** variables administradas manualmente en Vercel; cambios de schema realizados desde Supabase sin migraciones versionadas.
- **Rollback:** Vercel permite volver al deploy anterior en minutos; no equivale a rollback de datos y no hay procedimiento propio para la base.

## 4. Herramientas de Infraestructura

- **Vercel:** hosting y despliegue de Next.js.
- **Supabase:** PostgreSQL, Auth, RLS y correo de autenticación.
- **Resend:** correo transaccional de producto, con dominio no verificado documentado.
- **Ausencias relevantes:** no hay Docker, orquestador, CI, monitoreo, alertas, dashboard de errores, seed ni backups propios documentados.

## 5. Riesgos del Mapa de Entornos

- **Prueba sobre usuarios reales:** registros, turnos y correos persisten en producción.
- **Sin aislamiento:** desarrollo, demostraciones y eventual QA comparten el único entorno confirmado.
- **Protección de rutas:** después de cerrar sesión, las rutas de dashboard siguieron renderizando. No se ejecutaron escrituras para determinar si las APIs también quedan expuestas.
- **Sin puerta de calidad:** push a `main` puede desplegar sin lint ni tests automáticos.
- **Recuperación incompleta:** el código puede revertirse, pero los cambios de datos/schema no tienen rollback documentado.
- **Entregabilidad:** correos desde dominio de prueba pueden ir a spam y afectar journeys dependientes del enlace de cancelación.
- **Observabilidad:** los incidentes se detectan por soporte o revisión manual de logs.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| URL vigente, producción única y efecto irreversible | `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · La dirección y Lo del ambiente de UAT |
| Deploy, rollback, variables, monitoreo y ausencia de CI/tests | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Rendimiento, deploy y Lo que no está hecho |
| Stack y separación de APIs | `.context/architecture/system-design.md` · Stack e Interfaces |
| Login y registro accesibles | **Observado** — producción, 30/08/2026. Evidencia: snapshots Playwright de `/login`; sin envío de formularios |
| Cuenta profesional y rutas `/dashboard`, `/dashboard/availability`, `/dashboard/clients` | **Observado** — producción, 30/08/2026 mediante Playwright; exploración de solo lectura |
| Pantallas privadas renderizadas tras logout | **Observado** — producción, 30/08/2026 mediante Playwright; alcance sobre APIs no verificado |
| Matriz futura de compatibilidad | **Hipótesis pendiente de aprobación** — no existe definición documental |

## Contradicciones detectadas

- La especificación funcional y las notas técnicas de 2025 describen UAT y producción separados; la nota del 21/05/2026 afirma que UAT dejó de usarse. Se toma producción única como estado vigente.
- La especificación dice que UAT contiene datos ficticios; las notas técnicas describen copia parcial de producción y la nota más reciente indica pruebas sobre producción. No se presume aislamiento ni anonimización efectiva.
- Las notas hablan de rollback de deploy, mientras la nota QA advierte que los datos no pueden revertirse. Ambas son compatibles solo si se separa código de datos; el riesgo de datos permanece.

## Preguntas abiertas

- ¿Sigue existiendo el proyecto UAT y puede recuperarse sin datos reales?
- ¿Cuál es el procedimiento local real para ejecutar Next.js y Supabase?
- ¿Qué matriz de navegadores, dispositivos, resoluciones y accesibilidad debe soportarse?
- ¿Quién autoriza accesos de QA y dónde se almacenan las referencias de credenciales?
- ¿Qué controles deben bloquear un deploy y quién aprueba cambios de schema?
- ¿Qué RPO/RTO, backups, monitoreo y alertas requiere el producto?
- ¿La protección posterior a logout falla en routing, caché del cliente, renderizado o autorización de API?

## Próximo paso

Continuar con `.prompts/3-Infraestructura/data-strategy.md`.
