# Plan de Pruebas: Cancelaciones y comunicaciones transaccionales

**Epic:** CAQ-9
**Fecha:** 03/09/2026

## 1. Matriz de Riesgos del Producto

| ID | Riesgo | Probabilidad (1-5) | Impacto (1-5) | Nivel | Mitigación |
| :--- | :--- | :---: | :---: | :--- | :--- |
| R1 | Cancelación aparenta éxito sin persistir | 5 | 5 | 25 (Alto) | E2E con verificación API/DB y recarga |
| R2 | Slot cancelado no vuelve a ofrecerse | 5 | 4 | 20 (Alto) | Integración cancelación-disponibilidad |
| R3 | Token permite cancelar turno indebido | 3 | 5 | 15 (Alto) | Seguridad de token y autorización |
| R4 | Correos ausentes, duplicados o incorrectos | 4 | 4 | 16 (Alto) | Contratos, buzón controlado e idempotencia |
| R5 | Recordatorio no construido | 5 | 3 | 15 (Alto) | Decisión de release y prueba del scheduler |

## 2. Niveles de Prueba (Pyramid)

* **Unitarias:** Jest para transiciones, ventanas, tokens, destinatarios y deduplicación.
* **Integración:** Postman/Newman para appointments, disponibilidad, Resend y Supabase Auth.
* **E2E:** Playwright para ambas cancelaciones, recarga, slot liberado y correos.

## 3. Pruebas No Funcionales

* **Seguridad:** OWASP ZAP y pruebas dirigidas de entropía/vigencia de token, aislamiento y enumeración.
* **Resiliencia:** Postman/Newman para fallos y reintentos de Resend sin estados engañosos.
* **Performance:** k6 para propagación de cancelación; no hay SLA acordado.

## 4. Necesidades de Entorno y Datos

| Necesidad | Entorno | ¿Disponible hoy? | Referencia |
| :--- | :--- | :--- | :--- |
| Turnos futuros/pasados y buzones interceptados | Producción | No | `test-data-strategy.md` · Escenarios mínimos |
| Acceso de lectura a turno sintético existente | Producción | Parcial | `environments.md` · Detalles de Acceso |
| Control del reloj y scheduler | Producción | No | `test-data-strategy.md` · Capacidad faltante |

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Falla observada de CAQ-21 | `.context/PBI/epics/EPIC-CAQ-9-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-CAQ-21-cancelacion-por-profesional/story.md` |
| Restricción de entorno | `.context/infrastructure/environments.md` · Riesgos |
| Datos necesarios | `.context/infrastructure/test-data-strategy.md` · Escenarios mínimos |
| Scoring | **Hipótesis** — valoración de riesgo de QA |

## Contradicciones detectadas

* El comportamiento observado contradice persistencia y liberación; el recordatorio requerido fue excluido del lanzamiento.

## Preguntas abiertas

* ¿Qué ventana, zona, atomicidad de correo, release de recordatorios y entorno aislado se aprobarán?
