# Reporte de Inspección de Requisitos: Registro del profesional

**Historia:** CAQ-3
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-3-D1 | Completitud | No se define normalización de nombre y correo ni la unidad de sus máximos. | Acordar trim, comparación sin mayúsculas y conteo de caracteres. |
| CAQ-3-D2 | Caso borde | No se define la recuperación si cuenta, URL, sesión o correo fallan parcialmente. | Especificar atomicidad, reintentos y mensaje para cada fallo. |
| CAQ-3-D3 | Contradicción contra evidencia | La URL debe generarse, pero no se encontró cómo localizarla en la experiencia autenticada. | Separar generación de exposición y resolver CAQ-6. |

## 2. Versión Corregida de la Historia

Como profesional, quiero registrarme con nombre, correo y contraseña válidos, para crear una única cuenta, iniciar sesión y obtener una URL pública única. Se conservan los diez escenarios de `story.md`; la normalización, los fallos parciales y la exposición de la URL quedan marcados `Pendiente` y no deben asumirse como aprobados.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Reglas y escenarios inspeccionados | `.context/PBI/epics/EPIC-CAQ-2-cuenta-y-activacion-del-profesional/stories/STORY-CAQ-3-registro-del-profesional/story.md` |
| Registro, sesión y URL pública | `.context/architecture/prd.md` · Feature 1 |
| URL no localizada | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Feature 1 |

## Contradicciones detectadas

* La URL se genera según la especificación, pero no se encontró expuesta en el producto; generación y acceso no pueden considerarse el mismo resultado.

## Preguntas abiertas

* ¿Cómo se normalizan y cuentan nombre y correo?
* ¿Qué resultado corresponde a cada fallo parcial del alta?
