# Story: Como cliente final, quiero confirmar un turno sin crear una cuenta, para reservar con la menor fricción posible

**ID:** CAQ-18
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como cliente final, quiero confirmar un turno sin crear una cuenta, para reservar con la menor fricción posible.

## Criterios de Aceptación (Borrador)

- [ ] El cliente informa nombre y correo electrónico para reservar.
- [ ] El flujo no exige registro, contraseña ni aprobación previa del profesional.
- [ ] Antes de guardar, el sistema vuelve a comprobar que el horario sigue disponible.
- [ ] Una reserva válida crea el turno en estado `confirmed`.
- [ ] Después de confirmar, el cliente ve una confirmación de la operación.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Reserva con nombre y correo, sin cuenta | `.context/Confluence-corporativo/01-minuta-kickoff.md` · Los dos usuarios del sistema; `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 5.1 |
| Revalidación antes de guardar | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · RN-02 |
| Estado confirmado sin aprobación | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 9 |
