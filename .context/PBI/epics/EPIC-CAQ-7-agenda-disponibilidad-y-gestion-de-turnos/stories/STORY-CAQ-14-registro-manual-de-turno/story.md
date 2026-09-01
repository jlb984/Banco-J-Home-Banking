# Story: Como profesional, quiero registrar un turno manualmente, para incorporar reservas coordinadas fuera de la página pública

**ID:** CAQ-14
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero registrar un turno manualmente, para incorporar reservas coordinadas fuera de la página pública.

## Criterios de Aceptación (Borrador)

- [ ] El turno manual queda asociado con el profesional y con un cliente.
- [ ] El turno no puede ocupar un horario ya reservado.
- [ ] El turno nace en estado `confirmed`.
- [ ] Si la operación incorpora un cliente nuevo, se aplica el límite freemium.
- [ ] La selección de cliente y horario desde el panel permanece como borrador hasta documentar la interfaz real.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Existencia de turnos cargados manualmente | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · métricas del soft launch; `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · ticket #33 |
| Asociación, estado y ausencia de superposición | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Tablas y reserva; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 5.2 y 9 |
| Aplicación del límite a altas manuales | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 8.1 |
| Flujo del panel para seleccionar cliente y horario | **Hipótesis** — la documentación no describe la interfaz de carga manual |
