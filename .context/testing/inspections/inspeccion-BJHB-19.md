# Reporte de Inspección de Requisitos: Consulta de horarios disponibles

**Historia:** BJHB-19
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| BJHB-19-D1 | Completitud | No se define zona horaria ni límites de semana. | Acordar zona del profesional y conversión para clientes. |
| BJHB-19-D2 | Regla de negocio | No hay anticipación mínima ni máxima para reservar. | Definir ventanas reservables. |
| BJHB-19-D3 | Caso borde | No se define el estado vacío ni fallos del cálculo de slots. | Especificar mensaje y recuperación verificables. |

## 2. Versión Corregida de la Historia

Como cliente, quiero consultar una semana de slots futuros que no estén confirmados ni bloqueados. Zona horaria, ventanas de anticipación, estado vacío y fallos quedan `Pendiente`; no se ofrecen horarios pasados.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Escenarios inspeccionados | `.context/PBI/epics/EPIC-BJHB-4-pagina-publica-y-auto-reserva/stories/STORY-BJHB-19-consulta-de-horarios-disponibles/story.md` |
| Exclusiones de slots | `.context/architecture/prd.md` · Feature 3 |

## Contradicciones detectadas

* Ninguna detectada; la ausencia de zona horaria es un riesgo transversal del PRD.

## Preguntas abiertas

* ¿Qué zona, anticipación y respuesta sin horarios se aplican?
