# Story: Como cliente final, quiero conservar mis datos si otro cliente toma el horario, para elegir otro sin comenzar de nuevo

**ID:** CAQ-19
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como cliente final, quiero conservar mis datos si otro cliente toma el horario, para elegir otro sin comenzar de nuevo.

## Criterios de Aceptación (Borrador)

- [ ] El sistema rechaza la confirmación si el horario dejó de estar disponible.
- [ ] El mensaje informa que otra persona reservó el horario y solicita elegir otro.
- [ ] La disponibilidad se actualiza después del conflicto.
- [ ] El nombre y el correo ya ingresados se conservan.
- [ ] El sistema no crea dos turnos confirmados para el mismo profesional y horario.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Rechazo, mensaje, actualización y conservación de datos | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-02 |
| Garantía de no superposición | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-01 |
| Riesgo de implementación no transaccional | `.context/Confluence-corporativo/04-notas-tecnicas.md` · La reserva; `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · Horarios y disponibilidad |
