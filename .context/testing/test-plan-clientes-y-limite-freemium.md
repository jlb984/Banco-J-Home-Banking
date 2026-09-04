# Plan de Pruebas: Clientes y límite freemium

**Epic:** BJHB-6
**Fecha:** 03/09/2026

## 1. Matriz de Riesgos del Producto

| ID | Riesgo | Probabilidad (1-5) | Impacto (1-5) | Nivel | Mitigación |
| :--- | :--- | :---: | :---: | :--- | :--- |
| R1 | Conteo incorrecto bloquea o permite al cliente 11 | 4 | 5 | 20 (Alto) | Particiones 0/9/10/11 y normalización |
| R2 | Listado expone clientes de otro profesional | 3 | 5 | 15 (Alto) | RLS/API con dos profesionales |
| R3 | Alta manual no funciona o duplica clientes | 4 | 4 | 16 (Alto) | Integración UI/API y unicidad |
| R4 | CTA promete una oferta inexistente | 4 | 3 | 12 (Alto) | Prueba de contenido y ausencia de cobro |

## 2. Niveles de Prueba (Pyramid)

* **Unitarias:** Jest para normalización, conteo y transición 9/10/11.
* **Integración:** Postman/Newman para clients, appointments, RLS, alta manual y registro de interés.
* **E2E:** Playwright para listado, alta, reserva de existente/nuevo y CTA Plan Pro.

## 3. Pruebas No Funcionales

* **Seguridad:** OWASP ZAP y pruebas dirigidas de aislamiento y minimización de PII.
* **Performance:** k6 para listado y conteo creciente; no hay volumen objetivo.
* **Accesibilidad:** axe con Playwright para tabla, formulario, bloqueo y aviso permanente.

## 4. Necesidades de Entorno y Datos

| Necesidad | Entorno | ¿Disponible hoy? | Referencia |
| :--- | :--- | :--- | :--- |
| Fixtures con 0/9/10/11 clientes | Producción | No | `test-data-strategy.md` · Escenarios mínimos |
| Dos profesionales para RLS | Producción | No | `test-data-strategy.md` · Gestión de Usuarios |
| Cuenta observada con cero clientes | Producción | Parcial | `test-data-strategy.md` · Baseline observado |

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Límite y CTA | `.context/PBI/epics/EPIC-BJHB-6-clientes-y-limite-freemium/epic.md` y sus Stories |
| Riesgo PII | `.context/infrastructure/test-data-strategy.md` · Privacidad y Seguridad |
| Entorno único | `.context/infrastructure/environments.md` · Mapa de Entornos |
| Scoring | **Hipótesis** — valoración de riesgo de QA |

## Contradicciones detectadas

* La carga manual está en alcance, pero el botón observado no produjo ningún formulario; Plan Pro no existe como oferta definida.

## Preguntas abiertas

* ¿Cómo se normaliza el correo, qué bajas cuentan, dónde se registra interés y qué entorno aislado se usará?
