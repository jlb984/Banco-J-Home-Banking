# Story: Configuración de disponibilidad recurrente
**ID:** PBI-06
**Epic:** PBI-05
**Implementación:** Sin verificar
**Estado de sincronización:** PENDIENTE DE SUBIR A JIRA

## Descripción
Como profesional independiente, quiero configurar mis horarios de trabajo regulares para cada día de la semana, para que mis clientes solo vean horarios disponibles dentro de mis franjas laborales.

## Criterios de Aceptación (Borrador)
- [ ] El profesional puede activar o desactivar cada día (lunes a domingo) y asignarle bloques horarios (inicio y fin).
- [ ] La hora de fin de un bloque debe ser estrictamente posterior a la de inicio.
- [ ] Los bloques dentro de un mismo día no pueden solaparse.
- [ ] Al guardar, el sistema debe reemplazar la configuración completa existente (no es una actualización incremental).

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Reglas de disponibilidad y reemplazo de configuración | `03-especificacion-funcional-v0.3.md` · sección 4.1 |
| UI observada y falla al guardar | **Observado** — producción, 30/08/2026. Evidencia: `prd.md` · sección 3 Feature 2 |
