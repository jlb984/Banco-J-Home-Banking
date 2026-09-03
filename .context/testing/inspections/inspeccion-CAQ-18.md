# Reporte de Inspección de Requisitos: Confirmación de reserva sin cuenta

**Historia:** CAQ-18
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-18-D1 | Completitud | No se definen máximos ni normalización de nombre y correo. | Acordar particiones y mensajes. |
| CAQ-18-D2 | Integridad | No se define idempotencia ante reintento o doble clic. | Incorporar una clave o regla verificable contra duplicados. |
| CAQ-18-D3 | Completitud | No se especifican contenido ni persistencia de la confirmación visible. | Definir los datos mostrados tras reservar. |

## 2. Versión Corregida de la Historia

Como cliente sin cuenta, quiero confirmar una única reserva con nombre y correo válidos después de revalidar el slot. Máximos, normalización, idempotencia y contenido de confirmación quedan `Pendiente`.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Historia inspeccionada | `.context/PBI/epics/EPIC-CAQ-8-pagina-publica-y-auto-reserva/stories/STORY-CAQ-18-confirmacion-de-reserva-sin-cuenta/story.md` |
| Revalidación y estado `confirmed` | `.context/architecture/prd.md` · Feature 3 |
| Idempotencia | **Hipótesis** — no hay regla acordada |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué validaciones, protección contra reintentos y confirmación visual se requieren?
