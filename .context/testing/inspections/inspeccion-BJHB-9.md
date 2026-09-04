# Reporte de Inspección de Requisitos: Carga manual de cliente

**Historia:** BJHB-9
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-9-D1 | Contradice al sistema | «Nuevo Cliente» no produjo formulario ni cambio visible. | Confirmar si está roto, pendiente o condicionado. |
| BJHB-9-D2 | Regla de negocio | No se define el resultado para un correo ya asociado. | Acordar rechazo, reutilización o actualización. |
| BJHB-9-D3 | Completitud | Faltan máximos, normalización y mensajes. | Especificar validaciones y respuesta al límite. |

## 2. Versión Corregida de la Historia

Como profesional, quiero asociar manualmente un cliente nuevo mediante nombre y correo válidos, respetando el límite de diez. El tratamiento de existentes, validaciones y mensajes queda `Pendiente`; la función continúa sin verificación exitosa.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios inspeccionados | `.context/PBI/epics/EPIC-BJHB-6-clientes-y-limite-freemium/stories/STORY-BJHB-9-carga-manual-de-cliente/story.md` |
| Botón sin respuesta | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Feature 5 |

## Contradicciones detectadas

* La función está en el alcance, pero la acción observada no abrió el alta.

## Preguntas abiertas

* ¿La acción está rota, pendiente o condicionada, y cómo trata correos existentes?
