# Reporte de Inspección de Requisitos: Conflicto de reserva concurrente

**Historia:** BJHB-22
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-22-D1 | Contradicción técnica | Se exige unicidad, pero la validación documentada no es transaccional. | Hacer verificable una garantía atómica en persistencia. |
| BJHB-22-D2 | Completitud | No se define el texto literal ni accesibilidad del conflicto. | Acordar mensaje y anuncio de la actualización. |
| BJHB-22-D3 | Caso borde | No se define cuánto se conservan los datos ni si la unicidad cubre otros canales. | Acordar ciclo de vida y alcance global. |

## 2. Versión Corregida de la Historia

Como cliente, quiero que solo una solicitud gane un slot concurrente y que la perdedora conserve nombre y correo para elegir otro. Mensaje, duración de conservación y alcance entre canales quedan `Pendiente`; la unicidad debe comprobarse en persistencia.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Escenarios y riesgo técnico | `.context/PBI/epics/EPIC-BJHB-4-pagina-publica-y-auto-reserva/stories/STORY-BJHB-22-conflicto-de-reserva-concurrente/story.md` |
| Carrera conocida | `.context/architecture/prd.md` · Feature 3 y Riesgos |

## Contradicciones detectadas

* La garantía funcional de no superposición no está respaldada por el mecanismo técnico documentado.

## Preguntas abiertas

* ¿Qué mensaje, tiempo de conservación y alcance tiene la garantía de unicidad?
