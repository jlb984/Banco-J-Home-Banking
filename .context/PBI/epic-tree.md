# Índice del Backlog

**Origen:** `.context/architecture/prd.md`
**Fuentes del backlog:** `.context/Confluence-corporativo/`
**Tipo de proyecto:** Brownfield
**Fecha:** 2026-08-31

| Epic | Stories | Sin verificar | Estado de sincronización |
| :--- | :--- | :--- | :--- |
| PBI-01 Cuenta y activación del profesional | 3 | 3 | PENDIENTE DE SUBIR A JIRA |
| PBI-05 Agenda y disponibilidad | 3 | 3 | PENDIENTE DE SUBIR A JIRA |

## Epics identificadas, pendientes de desglosar
*   Página pública y auto-reserva — sale de `prd.md` · Feature 3 / `03-especificacion-funcional-v0.3.md`. Historias estimadas: 4
*   Cancelaciones y comunicaciones — sale de `prd.md` · Feature 4 / `03-especificacion-funcional-v0.3.md`. Historias estimadas: 3
*   Clientes y límite freemium — sale de `prd.md` · Feature 5 / `03-especificacion-funcional-v0.3.md`. Historias estimadas: 3

## Pendiente de subir a Jira
*   PBI-01 Cuenta y activación del profesional
*   PBI-02 Registro de cuenta y generación de URL
*   PBI-03 Inicio de sesión
*   PBI-04 Recuperación de contraseña
*   PBI-05 Agenda y disponibilidad
*   PBI-06 Configuración de disponibilidad recurrente
*   PBI-07 Configuración de duración de turno
*   PBI-08 Bloqueos de agenda

## Pendiente de verificar contra la aplicación
*   PBI-02 Registro de cuenta y generación de URL (Navegación e interfaz de la URL ausente)
*   PBI-03 Inicio de sesión (Pantallas de dashboard visibles sin sesión real)
*   PBI-04 Recuperación de contraseña (Recuperación no verificada)
*   PBI-06 Configuración de disponibilidad recurrente (La UI no guardó cambios observados)
*   PBI-07 Configuración de duración de turno (La UI no guardó cambios observados)
*   PBI-08 Bloqueos de agenda (La UI no guardó cambios observados)

## Contradicciones detectadas
*   La especificación (sección 3.2 y notas técnicas) menciona que el panel de control está protegido por middleware, pero el PRD (sección 5) observó que las rutas del dashboard siguen renderizando contenido sin sesión. Mantenemos el estado actual del PRD como lo observado y la especificación como lo esperado.

## Preguntas abiertas
*   ¿Qué ocurre si hay múltiples intentos de inicio de sesión fallidos? (Mencionado como TBD en la especificación).
*   ¿Las rutas de dashboard deben redirigir inmediatamente al login y limpiar todo contenido al cerrar sesión?
*   ¿Qué ocurre con turnos existentes al momento de que el profesional agrega un bloqueo sobre esa misma franja horaria? (TBD en la especificación).
