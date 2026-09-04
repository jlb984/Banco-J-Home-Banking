# Reporte de Inspección de Requisitos: Inicio y cierre de sesión

**Historia:** BJHB-11
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-11-D1 | Contradice al sistema | Tras logout se renderizaron rutas documentadas como protegidas. | Confirmar si fue caché o autorización y exigir que no se expongan datos. |
| BJHB-11-D2 | Completitud | No se define redirección, limpieza de UI ni alcance entre pestañas/dispositivos. | Acordar el estado posterior al logout. |
| BJHB-11-D3 | Seguridad | No existe política acordada para intentos fallidos o bloqueo temporal. | Definir rate limit y recuperación sin facilitar enumeración. |

## 2. Versión Corregida de la Historia

Como profesional, quiero iniciar y cerrar sesión, para acceder a mi panel sin exponer datos después de finalizarla. Los escenarios de acceso protegido se conservan como criterios candidatos; redirección, limpieza, propagación y bloqueo quedan `Pendiente` hasta decisión funcional y de seguridad.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios inspeccionados | `.context/PBI/epics/EPIC-BJHB-1-cuenta-y-activacion-del-profesional/stories/STORY-BJHB-11-inicio-y-cierre-de-sesion/story.md` |
| Dashboard protegido | `.context/architecture/prd.md` · Requisitos No Funcionales |
| Rutas renderizadas después del logout | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Seguridad observada |

## Contradicciones detectadas

* La protección declarada del dashboard contradice el renderizado observado después del logout; no se decide si falla la UI, la caché o la autorización.

## Preguntas abiertas

* ¿Qué debe mostrarse y qué datos deben eliminarse después del logout?
* ¿Cómo se limitan los intentos fallidos?
