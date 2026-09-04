# Reporte de Inspección de Requisitos: Registro manual de turno

**Historia:** BJHB-17
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-17-D1 | Completitud | No se definen campos ni validaciones del alta. | Especificar cliente, horario y datos obligatorios. |
| BJHB-17-D2 | Regla de negocio | No se aclara si admite horarios fuera de disponibilidad o bloqueados. | Acordar excepciones del profesional. |
| BJHB-17-D3 | Integridad | No se define idempotencia ante doble envío. | Incorporar una garantía contra duplicados. |

## 2. Versión Corregida de la Historia

Como profesional autenticado, quiero crear un único turno `confirmed` para un cliente y horario no ocupado. Los campos, excepciones de disponibilidad y comportamiento ante reenvíos quedan `Pendiente`; el límite de diez clientes se aplica a clientes nuevos.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios inspeccionados | `.context/PBI/epics/EPIC-BJHB-3-agenda-disponibilidad-y-gestion-de-turnos/stories/STORY-BJHB-17-registro-manual-de-turno/story.md` |
| Alcance de agenda | `.context/architecture/prd.md` · Feature 2 |
| Idempotencia | **Hipótesis** — no hay regla acordada |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué campos, excepciones de agenda y protección contra reenvíos se requieren?
