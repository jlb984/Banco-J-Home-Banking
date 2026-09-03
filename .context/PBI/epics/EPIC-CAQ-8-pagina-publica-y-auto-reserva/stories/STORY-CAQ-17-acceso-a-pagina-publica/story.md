# Story: Acceso a la página pública del profesional

**ID:** CAQ-17
**Epic:** CAQ-8
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como cliente final, quiero acceder a la página pública de un profesional, para identificar con quién voy a reservar.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede probarse con un perfil y slug existentes. |
| Negociable | Sí | Acceso y aislamiento están definidos; el contenido del perfil queda abierto. |
| Valiosa | Sí | Identifica al profesional antes de reservar. |
| Estimable | No | No están definidos los datos públicos ni el caso de slug inexistente. |
| Pequeña | Sí | Se limita a resolver y presentar una página pública. |
| Testeable | No | El acceso es verificable, pero falta el contenido esperado mínimo. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Abrir una página pública válida

**Given** que existe un profesional con un slug único
**When** el cliente abre `https://cita-ai.vercel.app/{slug}` sin iniciar sesión
**Then** el sistema presenta únicamente el perfil correspondiente al slug
**And** permite continuar a la consulta de disponibilidad

### Escenario 2: Aislar perfiles por slug

**Given** que existen dos profesionales con slugs diferentes
**When** el cliente abre la URL de uno de ellos
**Then** la página no expone datos privados ni datos del otro profesional

### Escenario 3: Consultar un slug inexistente

**Given** que el slug solicitado no corresponde a un profesional
**When** el cliente abre la URL pública
**Then** el sistema no presenta el perfil de ningún profesional

## Notas de QA

* Probar acceso anónimo, dos perfiles distintos y un slug inexistente.
* Revisar que la respuesta pública no incluya campos privados.
* La implementación continúa `Sin verificar`.

## Inspección Shift-Left

**Resultado:** Requiere Cambios

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-17.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Acceso público sin cuenta y por slug | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 2.2 y 3.4 |
| Consulta pública del perfil | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Row level security y endpoints públicos |
| Dominio vigente | `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · La dirección |
| Contenido visual exacto del perfil | **Hipótesis** — la documentación no enumera los datos visibles en la página |

## Contradicciones detectadas

* La especificación usa el dominio `cita.ai`; la nota de ambientes posterior establece `https://cita-ai.vercel.app/`. Se adopta el dominio vigente de la fuente más reciente.

## Preguntas abiertas

* ¿Qué datos del profesional deben mostrarse y cuáles deben permanecer privados?
* ¿Qué estado, mensaje y código HTTP corresponden a un slug inexistente?
* ¿Qué debe mostrarse si el profesional todavía no configuró disponibilidad?
