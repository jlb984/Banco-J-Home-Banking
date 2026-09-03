# Story: Confirmación de reserva sin cuenta

**ID:** CAQ-18
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como cliente final, quiero confirmar un turno sin crear una cuenta, para reservar con la menor fricción posible.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende de perfil público, disponibilidad y límite freemium. |
| Negociable | Sí | El flujo sin cuenta está definido; validaciones y confirmación visual quedan abiertas. |
| Valiosa | Sí | Reduce la fricción para concretar la reserva. |
| Estimable | Sí | Datos, revalidación y estado final están documentados. |
| Pequeña | Sí | Cubre una única confirmación de turno. |
| Testeable | Sí | Creación, estado, ausencia de cuenta y revalidación son comprobables. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Confirmar una reserva válida

**Given** que el cliente seleccionó un horario disponible
**And** informa su nombre y un correo electrónico válido
**When** confirma la reserva sin crear una cuenta
**Then** el sistema vuelve a comprobar la disponibilidad
**And** crea un único turno con estado `confirmed`
**And** muestra la confirmación de la operación sin requerir aprobación previa

### Escenario 2: Rechazar datos obligatorios inválidos

**Given** que el nombre está vacío o el correo está vacío o tiene formato inválido
**When** el cliente intenta confirmar
**Then** el sistema rechaza la solicitud
**And** no crea el turno

### Escenario 3: Rechazar un horario que dejó de estar disponible

**Given** que el horario seleccionado fue ocupado antes de la confirmación
**When** el cliente confirma la reserva
**Then** el sistema no crea el turno
**And** aplica el flujo de conflicto definido en CAQ-19

## Notas de QA

* Verificar que no se creen cuenta, contraseña ni sesión del cliente.
* Probar reenvío de formulario y conflicto concurrente.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-18.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Reserva con nombre y correo, sin cuenta | `.context/Confluence-corporativo/01-minuta-kickoff.md` · Los dos usuarios del sistema; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 5.1 |
| Revalidación antes de guardar | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-02 |
| Estado confirmado sin aprobación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 9 |
| Rechazo de nombre o correo inválidos | **Hipótesis** — no hay mensajes ni validaciones completas documentadas para este formulario |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Cuáles son los máximos y reglas de normalización de nombre y correo?
* ¿Qué mensaje confirma la reserva y qué datos contiene?
* ¿Cómo se evita crear duplicados ante reintentos de la misma solicitud?
