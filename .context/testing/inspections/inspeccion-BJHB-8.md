# Reporte de Inspección de Requisitos: Límite de diez clientes

**Historia:** BJHB-8
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-8-D1 | Regla de negocio | No se define normalización del correo para contar únicos. | Acordar una identidad canónica. |
| BJHB-8-D2 | Caso borde | No se define si cancelados o eliminados siguen contando. | Fijar ciclo de vida del contador. |
| BJHB-8-D3 | Completitud | El mensaje al cliente no tiene texto verificable. | Acordar contenido y canal de contacto. |

## 2. Versión Corregida de la Historia

Como responsable del producto, quiero limitar cada profesional gratuito a diez clientes únicos por correo, permitiendo reservas ilimitadas a los existentes y bloqueando al nuevo número once en ambos canales. Normalización, bajas y texto quedan `Pendiente`.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Regla y vacíos | `.context/PBI/epics/EPIC-BJHB-6-clientes-y-limite-freemium/stories/STORY-BJHB-8-limite-de-diez-clientes-unicos/story.md` |
| Límite y canales | `.context/architecture/prd.md` · Feature 5 |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Cómo se normalizan y depuran clientes del contador y cuál es el mensaje literal?
