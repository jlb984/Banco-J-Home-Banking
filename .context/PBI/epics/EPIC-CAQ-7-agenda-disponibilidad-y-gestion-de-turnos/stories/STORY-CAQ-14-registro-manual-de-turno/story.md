# Story: Registro manual de un turno

**ID:** CAQ-14
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero registrar un turno manualmente, para incorporar reservas coordinadas fuera de la página pública.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | No | Depende de clientes, disponibilidad y límite freemium. |
| Negociable | Sí | El resultado está definido; el flujo de selección sigue abierto. |
| Valiosa | Sí | Incorpora reservas acordadas por otros canales. |
| Estimable | No | No se definieron los campos ni si admite horarios fuera de disponibilidad. |
| Pequeña | Sí | Crea un turno desde el panel. |
| Testeable | No | La creación y superposición son comprobables, pero faltan reglas de entrada. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Registrar un turno manual válido

**Given** que el profesional está autenticado
**And** selecciona un cliente y un horario no reservado
**When** confirma el alta manual
**Then** el sistema crea un único turno asociado con ambos
**And** lo registra con estado `confirmed`

### Escenario 2: Rechazar un horario ocupado

**Given** que ya existe un turno confirmado del profesional en el horario elegido
**When** intenta registrar otro turno manual
**Then** el sistema rechaza la operación
**And** no crea un turno superpuesto

### Escenario 3: Aplicar el límite a un cliente nuevo

**Given** que el alta incorporaría un cliente único nuevo
**And** el profesional ya alcanzó diez clientes únicos
**When** intenta registrar el turno
**Then** el sistema rechaza la incorporación del nuevo cliente
**And** no crea el turno

## Notas de QA

* Probar cliente existente, cliente nuevo décimo y cliente nuevo número once.
* Validar ausencia de duplicados ante envíos repetidos.
* La implementación continúa `Sin verificar`.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Existencia de turnos cargados manualmente | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · métricas del soft launch; `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · ticket #33 |
| Asociación, estado y ausencia de superposición | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Tablas y reserva; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 5.2 y 9 |
| Aplicación del límite a altas manuales | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.1 |
| Flujo del panel para seleccionar cliente y horario | **Hipótesis** — la documentación no describe la interfaz de carga manual |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué datos se solicitan al crear un cliente durante el alta del turno?
* ¿Puede registrarse un turno fuera de la disponibilidad semanal o dentro de un bloqueo?
* ¿Qué comportamiento se espera ante el reenvío o doble clic de la misma operación?
