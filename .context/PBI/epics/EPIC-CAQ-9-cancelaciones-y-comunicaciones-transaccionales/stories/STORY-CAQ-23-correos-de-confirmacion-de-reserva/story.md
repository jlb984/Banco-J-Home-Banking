# Story: Correos de confirmación de la reserva

**ID:** CAQ-23
**Epic:** CAQ-9
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como participante de una reserva, quiero recibir su confirmación por correo, para conservar los datos del turno.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende de una reserva confirmada. |
| Negociable | Sí | Destinatarios y enlace están definidos; detalle y fallos siguen abiertos. |
| Valiosa | Sí | Deja constancia del turno para ambas partes. |
| Estimable | No | Faltan contenido obligatorio y manejo de fallas parciales. |
| Pequeña | Sí | Cubre los correos disparados por una reserva. |
| Testeable | Sí | Envíos, destinatarios y enlace pueden verificarse con buzones controlados. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Confirmar por correo al cliente

**Given** que se creó un turno `confirmed`
**When** el sistema procesa la nueva reserva
**Then** envía mediante Resend un correo al cliente con el detalle del turno
**And** incluye su enlace único de cancelación

### Escenario 2: Avisar al profesional

**Given** que se creó un turno `confirmed`
**When** el sistema procesa la nueva reserva
**Then** envía mediante Resend un aviso al profesional

### Escenario 3: Falla de entrega después de crear el turno

**Given** que el turno ya fue creado
**When** falla el envío de uno de los correos
**Then** el sistema conserva el turno `confirmed`
**And** no informa que la reserva completa falló

## Notas de QA

* Validar ambos buzones, datos del turno, enlace único y ausencia de credenciales.
* El escenario de falla es una hipótesis pendiente de ratificación.
* La implementación continúa `Sin verificar`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Destinatarios, detalle y enlace de cancelación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 7 |
| Proveedor vigente Resend | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · resumen del 03/03/2026 |
| Independencia entre creación y entrega | **Hipótesis** — las notas técnicas documentan envío sincrónico, pero no existe una regla acordada para fallas parciales |

## Contradicciones detectadas

* Las notas técnicas antiguas atribuyen todos los correos a Supabase; el hilo del 03/03/2026 migra los correos de producto a Resend. Se toma la fuente posterior.

## Preguntas abiertas

* ¿Qué detalle mínimo contiene cada correo y en qué zona horaria se expresa?
* ¿Qué política de reintentos y observabilidad se aplica a los fallos de Resend?
* ¿Negocio confirma que una falla de correo no revierte una reserva creada?
