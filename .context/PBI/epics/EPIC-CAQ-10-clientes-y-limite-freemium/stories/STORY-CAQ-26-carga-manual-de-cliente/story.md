# Story: Carga manual de un cliente

**ID:** CAQ-26
**Epic:** CAQ-10
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero cargar un cliente manualmente, para mantener completo mi registro.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende del listado y del límite freemium. |
| Negociable | Sí | Datos y límite están definidos; duplicados y validaciones quedan abiertos. |
| Valiosa | Sí | Completa el registro con clientes obtenidos fuera del flujo público. |
| Estimable | No | No se definió el resultado al ingresar un correo existente. |
| Pequeña | Sí | Cubre el alta de un cliente desde el panel. |
| Testeable | Sí | Alta, límite y aparición en listado son verificables. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Cargar un cliente nuevo dentro del límite

**Given** que el profesional está autenticado y tiene menos de diez clientes únicos
**And** informa nombre y un correo que no está asociado con su cuenta
**When** confirma el alta manual
**Then** el sistema asocia el cliente con el profesional
**And** lo muestra en su listado

### Escenario 2: Rechazar datos incompletos o inválidos

**Given** que el nombre está vacío o el correo está vacío o tiene formato inválido
**When** el profesional intenta crear el cliente
**Then** el sistema rechaza el alta
**And** no modifica el listado

### Escenario 3: Rechazar el cliente único número once

**Given** que el profesional ya tiene diez clientes únicos
**And** el correo informado corresponde a un cliente nuevo para él
**When** intenta cargarlo
**Then** el sistema rechaza el alta
**And** conserva el listado sin cambios

## Notas de QA

* Probar el décimo y undécimo cliente y un correo ya relacionado.
* Verificar aislamiento entre profesionales.
* La implementación continúa `Sin verificar`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Carga manual desde el panel | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 2.1 |
| Nombre, correo y unicidad | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Tablas |
| Aplicación del límite al alta manual | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 8.1 y 8.2 |
| Aparición inmediata en el listado | **Hipótesis** — es el resultado esperado del alta, pero la documentación no define la actualización de la interfaz |
| Rechazo de campos inválidos | **Hipótesis** — no hay reglas completas ni mensajes documentados |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué ocurre si el correo ya existe para ese profesional: se rechaza, actualiza o reutiliza?
* ¿Cuáles son los máximos y reglas de normalización de nombre y correo?
* ¿Qué mensaje se muestra al alcanzar el límite?
