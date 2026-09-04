# Reporte de Inspección de Requisitos: Página pública del profesional

**Historia:** BJHB-20
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-20-D1 | Privacidad | No se enumeran los datos públicos ni privados del perfil. | Definir una lista permitida de campos. |
| BJHB-20-D2 | Caso borde | No se define respuesta para slug inexistente. | Acordar estado, mensaje y código HTTP. |
| BJHB-20-D3 | Completitud | No se define la página sin disponibilidad configurada. | Especificar estado vacío sin habilitar reservas inválidas. |

## 2. Versión Corregida de la Historia

Como cliente anónimo, quiero abrir el perfil correspondiente a un slug válido sin exponer información privada. La lista de campos, respuesta de slug inexistente y estado sin disponibilidad quedan `Pendiente`.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Medio

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios y vacíos | `.context/PBI/epics/EPIC-BJHB-4-pagina-publica-y-auto-reserva/stories/STORY-BJHB-20-acceso-a-pagina-publica/story.md` |
| Página pública sin cuenta | `.context/architecture/prd.md` · Feature 3 |

## Contradicciones detectadas

* El dominio histórico difiere del vigente; la historia ya prioriza la fuente más reciente.

## Preguntas abiertas

* ¿Qué campos son públicos y qué respuestas corresponden a slug inexistente o sin disponibilidad?
