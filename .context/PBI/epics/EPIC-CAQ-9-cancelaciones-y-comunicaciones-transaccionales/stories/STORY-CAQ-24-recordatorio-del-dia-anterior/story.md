# Story: Como cliente final, quiero recibir un recordatorio el día anterior, para reducir el riesgo de olvidar el turno

**ID:** CAQ-24
**Epic:** CAQ-9
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como cliente final, quiero recibir un recordatorio el día anterior, para reducir el riesgo de olvidar el turno.

## Criterios de Aceptación (Borrador)

- [ ] El sistema identifica los turnos `confirmed` que ocurren al día siguiente.
- [ ] El cliente recibe un correo de recordatorio antes del turno.
- [ ] No se envían recordatorios para turnos `cancelled`.
- [ ] El proceso se ejecuta automáticamente sin intervención diaria del equipo.
- [ ] La hora exacta y la zona horaria de envío permanecen pendientes de definición.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Recordatorio del día anterior al cliente | `.context/Confluence-corporativo/01-minuta-kickoff.md` · Lo técnico; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 7 |
| Brecha confirmada y necesidad de ejecución programada | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · correo del 28/02/2026 |
| Demanda posterior al lanzamiento | `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · Recordatorios |
| Exclusión de turnos cancelados y automatización | **Hipótesis técnica** — se deducen del objetivo y de la necesidad de un proceso programado |
