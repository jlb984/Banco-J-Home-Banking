# Story: Límite de diez clientes únicos del plan gratuito

**ID:** BJHB-8
**Epic:** BJHB-6
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira (`BJHB`)
**Estado:** Refinado

## Descripción

Como responsable del producto, quiero limitar el plan gratuito a diez clientes únicos, para validar la intención de conversión.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Atraviesa la reserva pública y el alta manual. |
| Negociable | Sí | Límite, sujeto y excepciones están definidos. |
| Valiosa | Sí | Implementa la validación de intención de conversión. |
| Estimable | Sí | El umbral y los dos puntos de control están documentados. |
| Pequeña | Sí | Aplica una regla transversal acotada. |
| Testeable | Sí | Puede probarse en límites 9, 10 y 11 y con clientes existentes. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Permitir al décimo cliente único

**Given** que el profesional tiene nueve clientes únicos identificados por correo
**When** un cliente nuevo realiza una reserva válida
**Then** el sistema permite crear el turno
**And** contabiliza diez clientes únicos para ese profesional

### Escenario 2: Permitir nuevas reservas a un cliente existente

**Given** que el profesional ya tiene diez clientes únicos
**And** el correo pertenece a uno de ellos
**When** ese cliente realiza otra reserva válida
**Then** el sistema permite crear el turno sin límite de cantidad

### Escenario 3: Rechazar al undécimo cliente público

**Given** que el profesional ya tiene diez clientes únicos
**When** un cliente nuevo intenta reservar
**Then** el sistema rechaza la reserva
**And** le indica que contacte directamente al profesional

### Escenario 4: Rechazar al undécimo cliente manual

**Given** que el profesional ya tiene diez clientes únicos
**When** intenta cargar manualmente un correo nuevo
**Then** el sistema rechaza el alta

## Notas de QA

* Probar correos con diferencias de mayúsculas y espacios sin asumir normalización.
* Verificar que el conteo sea independiente por profesional.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-BJHB-8.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Límite, unicidad por correo y continuidad de clientes existentes | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.1 |
| Bloqueo de reserva y alta manual | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.2 |
| Mensaje al cliente nuevo bloqueado | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.2 |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Cómo se normaliza el correo para determinar clientes únicos?
* ¿Los clientes cancelados o eliminados continúan contando para el límite?
* ¿Cuál es el texto literal del mensaje de bloqueo?
