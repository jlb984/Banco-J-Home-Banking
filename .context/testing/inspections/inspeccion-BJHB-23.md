# Reporte de Inspección de Requisitos: Cancelación por enlace

**Historia:** BJHB-23
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-23-D1 | Seguridad | No se define vencimiento, revocación ni regeneración del token. | Acordar ciclo de vida y resistencia a manipulación. |
| BJHB-23-D2 | Regla de negocio | No existe ventana mínima de cancelación. | Definir hasta cuándo un turno futuro puede cancelarse. |
| BJHB-23-D3 | Caso borde | Faltan respuestas para token inválido, turno pasado o ya cancelado. | Especificar estados y mensajes verificables. |

## 2. Versión Corregida de la Historia

Como cliente sin cuenta, quiero cancelar un turno futuro mediante su enlace único, para persistir `cancelled` y liberar el slot. Ciclo del token, ventana mínima, idempotencia y mensajes quedan `Pendiente`.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios inspeccionados | `.context/PBI/epics/EPIC-BJHB-5-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-BJHB-23-cancelacion-por-cliente/story.md` |
| Cancelación futura y liberación | `.context/architecture/prd.md` · Feature 4 |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué vigencia, ventana, idempotencia y respuesta tiene el enlace?
