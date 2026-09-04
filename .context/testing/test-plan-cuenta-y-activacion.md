# Plan de Pruebas: Cuenta y activación del profesional

**Epic:** BJHB-1
**Fecha:** 03/09/2026

## 1. Matriz de Riesgos del Producto

| ID | Riesgo | Probabilidad (1-5) | Impacto (1-5) | Nivel | Mitigación |
| :--- | :--- | :---: | :---: | :--- | :--- |
| R1 | Acceso a datos después del logout | 4 | 5 | 20 (Alto) | Integración de autorización y E2E con dos cuentas |
| R2 | Registro parcial sin URL o sesión | 3 | 4 | 12 (Alto) | Pruebas de fallos parciales e idempotencia |
| R3 | Enumeración o abuso de recuperación | 3 | 5 | 15 (Alto) | Seguridad de mensajes, tokens y rate limit |
| R4 | URL pública no localizable | 4 | 4 | 16 (Alto) | E2E de activación y acceso al enlace |

## 2. Niveles de Prueba (Pyramid)

* **Unitarias:** Jest para validaciones, normalización y generación/colisión de slug.
* **Integración:** Postman/Newman para Supabase Auth, cookies, middleware, tokens y persistencia de perfil.
* **E2E:** Playwright para registro, login, recuperación, logout y localización de URL.

## 3. Pruebas No Funcionales

* **Seguridad:** OWASP ZAP y pruebas dirigidas de enumeración, fijación/revocación de sesión, autorización y abuso de tokens.
* **Performance:** k6 para medir registro, login y recuperación; no existe SLA acordado.
* **Accesibilidad:** axe con Playwright para formularios, errores y foco; no existe estándar acordado.

## 4. Necesidades de Entorno y Datos

| Necesidad | Entorno | ¿Disponible hoy? | Referencia |
| :--- | :--- | :--- | :--- |
| Dos profesionales sintéticos y buzones controlados | Producción | No | `test-data-strategy.md` · Gestión de Usuarios |
| Control de tokens, reloj y fallos de correo | Producción | No | `test-data-strategy.md` · Fuentes de Datos |
| Exploración de solo lectura con cuenta de prueba | Producción | Parcial | `environments.md` · Detalles de Acceso |

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Riesgos funcionales | `.context/PBI/epics/EPIC-BJHB-1-cuenta-y-activacion-del-profesional/epic.md` y sus Stories |
| Entorno único | `.context/infrastructure/environments.md` · Mapa de Entornos |
| Datos mutantes no disponibles | `.context/infrastructure/test-data-strategy.md` · Fuentes de Datos |
| Probabilidad, impacto y nivel | **Hipótesis** — valoración de riesgo de QA |

## Contradicciones detectadas

* El dashboard está documentado como protegido, pero se observó renderizado tras logout.

## Preguntas abiertas

* ¿Qué entorno aislado, política de sesiones, SLA y matriz de accesibilidad se aprobarán?
