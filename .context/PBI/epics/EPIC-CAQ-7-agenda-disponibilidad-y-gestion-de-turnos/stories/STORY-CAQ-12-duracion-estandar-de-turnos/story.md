# Story: Como profesional, quiero definir la duración estándar de mis turnos, para generar horarios acordes con mi servicio

**ID:** CAQ-12
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero definir la duración estándar de mis turnos, para generar horarios acordes con mi servicio.

## Criterios de Aceptación (Borrador)

- [ ] El profesional puede definir una duración en minutos.
- [ ] La duración debe ser mayor que cero.
- [ ] La misma duración se aplica a todos los turnos del profesional.
- [ ] La duración divide cada bloque de disponibilidad en horarios consecutivos.
- [ ] La restricción a valores predeterminados no se considera acordada hasta resolver la contradicción entre especificación e interfaz.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Duración positiva, única y usada para dividir la franja | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.2 |
| Opciones observadas de 15 a 120 minutos | `.context/architecture/prd.md` · Feature 2 |
| Conjunto definitivo de duraciones permitidas | **Hipótesis pendiente** — la especificación admite cualquier entero y la UI observada presenta opciones cerradas |
