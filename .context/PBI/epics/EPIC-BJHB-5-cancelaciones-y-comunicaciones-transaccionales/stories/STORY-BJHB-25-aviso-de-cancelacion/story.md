# Story: Aviso de cancelación a la contraparte

**ID:** BJHB-25
**Epic:** BJHB-5
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)
**Estado:** Refinado

## Descripción

Como parte de un turno cancelado, quiero recibir un aviso, para conocer el cambio.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende de una cancelación exitosa de BJHB-23 o BJHB-24. |
| Negociable | Sí | Destinatario y contenido mínimo están definidos. |
| Valiosa | Sí | Informa oportunamente el cambio a la contraparte. |
| Estimable | No | No existe regla acordada para fallas de entrega. |
| Pequeña | Sí | Cubre la notificación derivada de cancelar. |
| Testeable | Sí | Destinatario, contenido y ausencia de envío al actor son comprobables. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Avisar al profesional cuando cancela el cliente

**Given** que el cliente cancela exitosamente un turno
**When** el sistema procesa la cancelación
**Then** envía al profesional un aviso que identifica que canceló el cliente
**And** no envía ese aviso al cliente que inició la acción

### Escenario 2: Avisar al cliente cuando cancela el profesional

**Given** que el profesional cancela exitosamente un turno
**When** el sistema procesa la cancelación
**Then** envía al cliente un aviso que identifica que canceló el profesional
**And** no envía ese aviso al profesional que inició la acción

### Escenario 3: Falla de entrega posterior a la cancelación

**Given** que el turno ya cambió a `cancelled`
**When** falla el envío del aviso
**Then** el sistema conserva el estado cancelado

## Notas de QA

* Usar buzones sintéticos y comprobar destinatario, ausencia de duplicados y contenido.
* El escenario de falla conserva el turno por hipótesis y requiere ratificación.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-BJHB-25.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Destinatario y contenido del aviso | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 6.3 y 7 |
| Existencia actual del correo de cancelación | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · correo del 28/02/2026 |
| Manejo de una falla de correo posterior a cancelar | **Hipótesis** — la documentación indica envíos sincrónicos, pero no define atomicidad entre estado y notificación |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué datos del turno debe contener el aviso?
* ¿Cuántos reintentos se realizan ante una falla y cómo se informa al actor?
* ¿Negocio confirma que una falla de correo no revierte la cancelación?
