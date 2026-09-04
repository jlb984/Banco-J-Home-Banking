# Reporte de Inspección de Requisitos: Correos de confirmación

**Historia:** BJHB-27
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-27-D1 | Completitud | No se define el detalle obligatorio ni zona horaria de los correos. | Acordar contenido por destinatario. |
| BJHB-27-D2 | Resiliencia | No existe política de reintentos, duplicados ni trazabilidad. | Definir entrega observable e idempotente. |
| BJHB-27-D3 | Contradicción documental | Fuentes antiguas usan Supabase y la decisión posterior usa Resend. | Mantener Resend para correos de producto. |
| BJHB-27-D4 | Hipótesis no aprobada | No revertir la reserva ante fallo no está acordado. | Ratificar la atomicidad funcional. |

## 2. Versión Corregida de la Historia

Como participante, quiero recibir por Resend la confirmación de una reserva creada; el cliente además recibe enlace único de cancelación. Contenido, zona, reintentos, duplicados y efecto de fallos quedan `Pendiente`.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios y contradicciones | `.context/PBI/epics/EPIC-BJHB-5-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-BJHB-27-correos-de-confirmacion-de-reserva/story.md` |
| Correos transaccionales | `.context/architecture/prd.md` · Feature 4 |

## Contradicciones detectadas

* Se prioriza la migración posterior a Resend sobre las notas históricas de Supabase.

## Preguntas abiertas

* ¿Qué contenido, zona, reintentos y atomicidad corresponden a los correos?
