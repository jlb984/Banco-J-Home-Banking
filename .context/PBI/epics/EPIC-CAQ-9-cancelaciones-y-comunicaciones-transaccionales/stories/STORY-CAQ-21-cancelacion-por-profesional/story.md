# Story: Como profesional, quiero cancelar un turno desde mi panel, para actualizar mi agenda

**ID:** CAQ-21
**Epic:** CAQ-9
**Implementación:** Parcial
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero cancelar un turno desde mi panel, para actualizar mi agenda.

## Criterios de Aceptación (Borrador)

- [x] El profesional autenticado puede iniciar la cancelación desde un turno de su agenda.
- [ ] El profesional solo puede cancelar turnos asociados con su cuenta.
- [ ] No se puede cancelar un turno pasado.
- [ ] La cancelación cambia el estado a `cancelled` y libera el horario.
- [x] El motivo de cancelación no se exige mientras negocio no defina esa regla.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Cancelación desde el panel | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 2.1 y 6.2 |
| Aislamiento por profesional | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Row level security |
| Restricción temporal, estado y liberación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.3 |
| Motivo de cancelación | **Pregunta abierta** — `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.3 |
| Inicio de la cancelación desde una cita futura y ausencia de campo de motivo | **Observado** — producción, 02/09/2026, cuenta profesional con datos sintéticos. Evidencia: `evidence/2026-09-02-turno-futuro-con-accion-cancelar.png` |
| Retiro inmediato de la cita después de confirmar | **Observado** — producción, 02/09/2026. Evidencia: `evidence/2026-09-02-turno-cancelado-retirado-de-proximas-citas.png` |
| Falta de persistencia y de liberación del horario | **Observado** — producción, 02/09/2026. Evidencia: `evidence/2026-09-02-turno-reaparece-tras-recarga-sin-cache.png`, `evidence/2026-09-02-api-turno-permanece-confirmed.png`, `evidence/2026-09-02-slot-cancelado-no-disponible-en-pagina-publica.png` y `evidence/2026-09-02-api-slot-cancelado-no-liberado.png` |

## Comportamiento observado

| Qué hace | Evidencia | Qué decía la documentación |
| :--- | :--- | :--- |
| En una inspección previa del mismo día, la ruta `/dashboard` mostró `Próximas Citas` vacía. Esa observación no permitió recorrer la cancelación. | `evidence/2026-09-02-dashboard-sin-turnos-para-cancelar.png` | La especificación funcional indica que el profesional cancela desde su panel (`.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 6.2). |
| En la sesión autenticada actual, `Próximas Citas` mostró siete turnos futuros sintéticos `Prueba QA 1`; cada uno ofrecía las acciones `Contactar` y `Cancelar`. | `evidence/2026-09-02-turno-futuro-con-accion-cancelar.png` | Coincide con la cancelación desde el panel prevista en la sección 6.2 de la especificación funcional. |
| Al iniciar la cancelación del turno del 3 de septiembre a las 07:00, la aplicación mostró el texto literal “¿Estás seguro de que deseas cancelar esta cita? Esta acción no se puede deshacer.” en un diálogo nativo del navegador y no solicitó motivo. Al aceptar, retiró inmediatamente ese turno de la lista. El diálogo no pudo capturarse porque Playwright bloquea las capturas mientras está abierto; el estado anterior y posterior sí quedó evidenciado. | `evidence/2026-09-02-turno-futuro-con-accion-cancelar.png` y `evidence/2026-09-02-turno-cancelado-retirado-de-proximas-citas.png` | La documentación deja el motivo como `TBD`; no exige confirmación ni define su texto. |
| La cancelación no persistió: una navegación nueva del dashboard volvió a mostrar el mismo turno y `GET /api/appointments` lo devolvió con `status: "confirmed"`. | `evidence/2026-09-02-turno-reaparece-tras-recarga-sin-cache.png` y `evidence/2026-09-02-api-turno-permanece-confirmed.png` | Contradice la sección 6.3, que exige que el turno pase a estado cancelado. |
| El horario tampoco volvió a la oferta pública: para el 3 de septiembre se ofrecieron 09:00, 09:30 y luego 10:30, pero no 10:00, instante UTC del turno que el dashboard presentó como 07:00 en `America/Buenos_Aires`. La respuesta de `GET /api/public/availability` confirmó la misma ausencia. | `evidence/2026-09-02-slot-cancelado-no-disponible-en-pagina-publica.png` y `evidence/2026-09-02-api-slot-cancelado-no-liberado.png` | Contradice la sección 6.3, que exige que el horario vuelva a estar disponible. |

## Contradicciones detectadas

- La especificación funcional exige que el turno pase a cancelado, pero la UI solo lo retiró temporalmente: una navegación nueva volvió a mostrarlo y el endpoint autenticado mantuvo `status: "confirmed"`.
- La especificación funcional exige liberar el horario, pero la página y el endpoint público siguieron omitiendo las 10:00 del 3 de septiembre después del intento de cancelación.

## Preguntas abiertas

- ¿Qué mensaje aparece si se intenta cancelar un turno pasado o ya cancelado?
- ¿Por qué `POST /api/appointments/[id]/cancel` responde como exitoso y la UI retira el turno, pero el registro permanece `confirmed` y reaparece al abrir una navegación nueva?
- ¿La notificación de cancelación se intentó enviar aunque el estado no cambiara? ¿Qué recibió el buzón sintético?
- ¿La operación impide efectivamente cancelar turnos de otra cuenta? No se probó ese acceso porque el único entorno disponible es producción.
- ¿Negocio confirma que el profesional puede cancelar sin indicar un motivo, tal como funciona hoy?
- ¿Cómo debe presentarse la hora entre el dashboard (`07:00` en `America/Buenos_Aires`) y la página pública/API (`10:00Z`)?
