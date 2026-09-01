# Story: Como profesional, quiero encontrar mi URL pública, para compartirla con mis clientes

**ID:** CAQ-6
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira

## Descripción

Como profesional, quiero encontrar mi URL pública, para compartirla con mis clientes.

## Criterios de Aceptación (Borrador)

- [ ] El sistema genera el slug a partir del nombre en minúsculas, sin acentos y con los espacios reemplazados por guiones.
- [ ] El slug es único en toda la plataforma y, ante una colisión, incorpora un sufijo numérico incremental.
- [ ] La URL utiliza el dominio vigente `https://cita-ai.vercel.app/` seguido por el slug del profesional.
- [ ] El profesional puede localizar su URL pública desde su experiencia autenticada.
- [ ] La interfaz ofrece una forma directa de copiar la URL para compartirla.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Normalización y unicidad del slug | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.4 |
| Dominio vigente de las páginas públicas | `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · La dirección |
| La URL debe estar disponible para que el profesional pueda compartirla | `.context/architecture/prd.md` · Feature 1 y User Journeys; `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · Registro y acceso |
| Acción específica para copiar la URL | **Hipótesis** — el PRD identifica la consulta/copia como gap, pero la documentación no define el control de interfaz |
