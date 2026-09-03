# Story: Listado de clientes del profesional

**ID:** CAQ-25
**Epic:** CAQ-10
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero consultar mi listado de clientes, para conocer a las personas que reservaron conmigo.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede probarse con clientes y turnos preparados. |
| Negociable | Sí | Alcance y unicidad están definidos; orden e historial quedan abiertos. |
| Valiosa | Sí | Permite reconocer la base de clientes del profesional. |
| Estimable | No | No se definieron orden, búsqueda, paginación ni datos adicionales. |
| Pequeña | Sí | Se limita a la consulta de clientes asociados. |
| Testeable | Sí | Asociación, aislamiento y unicidad por correo son comprobables. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Consultar clientes propios

**Given** que el profesional autenticado tiene turnos asociados con clientes
**When** abre su listado de clientes
**Then** el sistema muestra el nombre y correo de esos clientes
**And** no incluye clientes sin relación con el profesional

### Escenario 2: Unificar un cliente con varios turnos

**Given** que el mismo correo está asociado con varios turnos del profesional
**When** consulta el listado
**Then** el sistema presenta una única entrada para ese correo

### Escenario 3: Aislar clientes de otro profesional

**Given** que un cliente reservó únicamente con otro profesional
**When** el profesional autenticado consulta su listado
**Then** el sistema no expone ese cliente

## Notas de QA

* Preparar dos profesionales, correos repetidos y múltiples turnos.
* No asumir historial, filtros ni paginación como parte de esta historia.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-25.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Listado de clientes | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.1 |
| Asociación por turnos y unicidad por correo | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Tablas y límite del plan gratuito |
| Nombre y correo del cliente | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.2 |
| Historial por cliente | **Pregunta abierta** — aparece como necesidad en entrevistas, pero no forma parte del comportamiento especificado |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Cómo se normaliza el correo para determinar unicidad?
* ¿Qué orden, búsqueda y paginación necesita el listado?
* ¿Se incluirá historial de turnos y, de ser así, con qué alcance?
