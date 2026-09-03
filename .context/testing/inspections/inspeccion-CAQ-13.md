# Reporte de Inspección de Requisitos: Bloqueo de períodos

**Historia:** CAQ-13
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-13-D1 | Regla de negocio | No se define qué ocurre con turnos confirmados dentro del bloqueo. | Acordar rechazo, advertencia o cancelación explícita. |
| CAQ-13-D2 | Caso borde | No se definen bloqueos pasados, superpuestos o que crucen medianoche. | Establecer validaciones por partición. |
| CAQ-13-D3 | Completitud | Falta zona horaria para inicio y fin. | Definir zona del profesional y representación. |

## 2. Versión Corregida de la Historia

Como profesional, quiero crear, consultar y eliminar bloqueos con inicio anterior al fin, para retirar slots de nuevas reservas. El tratamiento de turnos existentes, superposiciones, pasado y zona horaria queda `Pendiente`; no se cancelan turnos silenciosamente.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Vacíos y escenarios | `.context/PBI/epics/EPIC-CAQ-7-agenda-disponibilidad-y-gestion-de-turnos/stories/STORY-CAQ-13-bloqueo-de-periodos/story.md` |
| Regla pendiente | `.context/architecture/prd.md` · Feature 2 |

## Contradicciones detectadas

* Ninguna documental; existe una regla crítica sin definir.

## Preguntas abiertas

* ¿Qué ocurre con turnos existentes y qué zona/límites rigen el bloqueo?
