# Reporte de Inspección de Requisitos: Inicio y cierre de sesión

**Historia:** CAQ-4
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-4-D1 | Contradice al sistema | Tras logout se renderizaron rutas documentadas como protegidas. | Confirmar si fue caché o autorización y exigir que no se expongan datos. |
| CAQ-4-D2 | Completitud | No se define redirección, limpieza de UI ni alcance entre pestañas/dispositivos. | Acordar el estado posterior al logout. |
| CAQ-4-D3 | Seguridad | No existe política acordada para intentos fallidos o bloqueo temporal. | Definir rate limit y recuperación sin facilitar enumeración. |

## 2. Versión Corregida de la Historia

Como profesional, quiero iniciar y cerrar sesión, para acceder a mi panel sin exponer datos después de finalizarla. Los escenarios de acceso protegido se conservan como criterios candidatos; redirección, limpieza, propagación y bloqueo quedan `Pendiente` hasta decisión funcional y de seguridad.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Criterios inspeccionados | `.context/PBI/epics/EPIC-CAQ-2-cuenta-y-activacion-del-profesional/stories/STORY-CAQ-4-inicio-y-cierre-de-sesion/story.md` |
| Dashboard protegido | `.context/architecture/prd.md` · Requisitos No Funcionales |
| Rutas renderizadas después del logout | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Seguridad observada |

## Contradicciones detectadas

* La protección declarada del dashboard contradice el renderizado observado después del logout; no se decide si falla la UI, la caché o la autorización.

## Preguntas abiertas

* ¿Qué debe mostrarse y qué datos deben eliminarse después del logout?
* ¿Cómo se limitan los intentos fallidos?
