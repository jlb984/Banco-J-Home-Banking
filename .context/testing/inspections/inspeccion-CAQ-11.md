# Reporte de Inspección de Requisitos: Disponibilidad semanal

**Historia:** CAQ-11
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-11-D1 | Completitud | No se define la zona horaria de los bloques. | Acordar zona de almacenamiento y presentación. |
| CAQ-11-D2 | Caso borde | No se define si se permiten bloques contiguos o que crucen medianoche. | Fijar límites y ejemplos verificables. |
| CAQ-11-D3 | Resiliencia | No se especifica el resultado ante fallo del guardado completo. | Exigir atomicidad, conservación anterior y mensaje. |

## 2. Versión Corregida de la Historia

Como profesional, quiero reemplazar mi disponibilidad semanal con bloques válidos y no solapados, para ofrecer solo horarios atendibles. Zona horaria, medianoche, contigüidad y mensajes quedan `Pendiente`; un fallo no debe dejar una configuración parcial.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Medio

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Reglas inspeccionadas | `.context/PBI/epics/EPIC-CAQ-7-agenda-disponibilidad-y-gestion-de-turnos/stories/STORY-CAQ-11-configuracion-de-disponibilidad-semanal/story.md` |
| Reemplazo y exclusión de slots | `.context/architecture/prd.md` · Feature 2 |
| Atomicidad del reemplazo | **Hipótesis** — no hay manejo de fallo acordado |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué zona horaria, límites de día y mensajes se aplican?
