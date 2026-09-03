# Reporte de Inspección de Requisitos: Duración estándar

**Historia:** CAQ-12
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-12-D1 | Contradicción | La especificación admite cualquier entero positivo y la UI solo seis valores. | Producto debe fijar el dominio válido. |
| CAQ-12-D2 | Completitud | No se define el efecto sobre turnos futuros al cambiar la duración. | Preservar o recalcular explícitamente. |
| CAQ-12-D3 | Caso borde | No se acuerda cómo tratar el remanente de un bloque. | Definir si se descarta y con qué regla. |

## 2. Versión Corregida de la Historia

Como profesional, quiero definir una duración estándar admitida para dividir mis bloques en turnos completos. El conjunto admitido, el remanente y el efecto sobre turnos existentes quedan `Pendiente`; no se transforma la UI observada en regla de negocio.

## 3. Valoración de Calidad

* **Estado:** Bloqueante
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Contradicción y criterios | `.context/PBI/epics/EPIC-CAQ-7-agenda-disponibilidad-y-gestion-de-turnos/stories/STORY-CAQ-12-duracion-estandar-de-turnos/story.md` |
| Opciones observadas | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Feature 2 |

## Contradicciones detectadas

* Entero positivo documentado frente a opciones 15, 30, 45, 60, 90 y 120 observadas.

## Preguntas abiertas

* ¿Qué duraciones son válidas y qué ocurre con remanentes y turnos existentes?
