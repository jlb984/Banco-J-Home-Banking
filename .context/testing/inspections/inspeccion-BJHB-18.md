# Reporte de Inspección de Requisitos: Consulta de próximos turnos

**Historia:** BJHB-18
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-18-D1 | Seguridad observada | El dashboard renderizó sin sesión visible; no se comprobó aislamiento. | Verificar autorización de API y datos con dos cuentas. |
| BJHB-18-D2 | Completitud | No se definen campos, orden, filtros ni inclusión de cancelados. | Acordar contenido mínimo y orden temporal. |
| BJHB-18-D3 | Cobertura observada | Solo se observó el estado vacío, no una lista poblada. | Mantener la implementación como `Sin verificar`. |

## 2. Versión Corregida de la Historia

Como profesional con sesión válida, quiero consultar únicamente mis próximos turnos. Se conserva el estado vacío observado; campos, orden, filtros y tratamiento de `cancelled` quedan `Pendiente`, y el aislamiento requiere verificación antes de aprobar.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Historia y evidencia | `.context/PBI/epics/EPIC-BJHB-3-agenda-disponibilidad-y-gestion-de-turnos/stories/STORY-BJHB-18-consulta-de-proximos-turnos/story.md` |
| Dashboard protegido | `.context/architecture/prd.md` · Requisitos No Funcionales |
| Estado vacío | **Observado** — producción, 02/09/2026. Evidencia: `.context/PBI/epics/EPIC-BJHB-3-agenda-disponibilidad-y-gestion-de-turnos/stories/STORY-BJHB-18-consulta-de-proximos-turnos/evidence/2026-09-02-dashboard-sin-citas.png` |

## Contradicciones detectadas

* La protección documentada no coincide con el renderizado observado sin sesión visible; no se conoce si hubo exposición de datos.

## Preguntas abiertas

* ¿Qué contenido y orden tiene la lista y cómo se garantiza el aislamiento?
