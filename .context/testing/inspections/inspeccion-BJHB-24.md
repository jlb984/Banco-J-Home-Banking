# Reporte de Inspección de Requisitos: Cancelación por el profesional

**Historia:** BJHB-24
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-24-D1 | Contradice al sistema | La UI retiró el turno, pero la API lo mantuvo `confirmed`. | Corregir o explicar la persistencia antes de aprobar. |
| BJHB-24-D2 | Contradice al sistema | El horario no volvió a la disponibilidad pública. | Validar liberación en la misma operación persistente. |
| BJHB-24-D3 | Seguridad | No se verificó que un profesional no pueda cancelar turnos ajenos. | Probar autorización con dos cuentas en entorno aislado. |
| BJHB-24-D4 | Regla de negocio | El motivo y la ventana de cancelación siguen sin definición. | Obtener decisión de Producto. |

## 2. Versión Corregida de la Historia

Como profesional autenticado, quiero cancelar un turno futuro propio, para persistir `cancelled`, retirarlo de próximas citas y liberar el horario. El motivo, la ventana y los mensajes quedan `Pendiente`; el retiro optimista de UI no constituye éxito sin persistencia.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios y evidencia completa | `.context/PBI/epics/EPIC-BJHB-5-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-BJHB-24-cancelacion-por-profesional/story.md` |
| Persistencia fallida | **Observado** — producción, 02/09/2026. Evidencia: `.context/PBI/epics/EPIC-BJHB-5-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-BJHB-24-cancelacion-por-profesional/evidence/2026-09-02-api-turno-permanece-confirmed.png` |
| Slot no liberado | **Observado** — producción, 02/09/2026. Evidencia: `.context/PBI/epics/EPIC-BJHB-5-cancelaciones-y-comunicaciones-transaccionales/stories/STORY-BJHB-24-cancelacion-por-profesional/evidence/2026-09-02-api-slot-cancelado-no-liberado.png` |

## Contradicciones detectadas

* El criterio exige persistencia y liberación; ambos resultados contradicen el comportamiento observado.

## Preguntas abiertas

* ¿Cuál es la causa de la falsa respuesta exitosa y se envió una notificación incorrecta?
* ¿Qué motivo, ventana y autorización deben aplicarse?
