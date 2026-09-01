# Story: Como profesional, quiero configurar mi disponibilidad semanal, para ofrecer únicamente los horarios en los que atiendo

**ID:** CAQ-11
**Epic:** CAQ-7
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero configurar mi disponibilidad semanal, para ofrecer únicamente los horarios en los que atiendo.

## Criterios de Aceptación (Borrador)

- [ ] El profesional puede definir bloques de atención para cada día de la semana.
- [ ] Cada bloque exige que la hora de fin sea posterior a la hora de inicio.
- [ ] Los bloques de un mismo día no pueden solaparse.
- [ ] Al guardar, la configuración enviada reemplaza por completo las reglas anteriores.
- [ ] La disponibilidad pública se calcula únicamente a partir de las reglas vigentes.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Configuración por día y validaciones de los bloques | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.1 |
| Reemplazo completo al guardar | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 4.1; `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · Horarios |
| Uso de las reglas para calcular slots | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Los slots |
