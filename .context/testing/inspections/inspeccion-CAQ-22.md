# Reporte de Inspección de Requisitos: Aviso de cancelación

**Historia:** CAQ-22
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-22-D1 | Completitud | No se define el contenido mínimo del aviso. | Acordar identidad, fecha, hora y zona. |
| CAQ-22-D2 | Resiliencia | No hay política de reintentos ni observabilidad. | Definir estados de entrega y recuperación. |
| CAQ-22-D3 | Hipótesis no aprobada | La conservación de la cancelación ante fallo de correo no está acordada. | Ratificar atomicidad entre estado y notificación. |

## 2. Versión Corregida de la Historia

Como contraparte de un turno cancelado, quiero recibir un único aviso que identifique al actor y al turno. Contenido, reintentos y atomicidad quedan `Pendiente`; no se presenta como acordado conservar o revertir ante fallo.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Historia inspeccionada | `.context/PBI/epics/EPIC-CAQ-9-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-CAQ-22-aviso-de-cancelacion/story.md` |
| Aviso a quien no canceló | `.context/architecture/prd.md` · Feature 4 |

## Contradicciones detectadas

* Ninguna detectada; la atomicidad es una hipótesis explícita.

## Preguntas abiertas

* ¿Qué contiene el aviso y qué ocurre si Resend falla?
