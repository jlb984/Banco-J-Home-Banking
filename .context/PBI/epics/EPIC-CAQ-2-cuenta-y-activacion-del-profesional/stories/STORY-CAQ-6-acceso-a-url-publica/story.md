# Story: Acceso a la URL pública del profesional

**ID:** CAQ-6
**Epic:** CAQ-2
**Implementación:** Sin verificar
**Estado de sincronización:** Sincronizado con Jira
**Estado:** Refinado

## Descripción

Como profesional, quiero localizar y copiar mi URL pública desde la experiencia autenticada, para compartir mi página de reservas con mis clientes.

## Análisis INVEST

| Criterio | Cumple | Observación |
| :--- | :--- | :--- |
| Independiente | Sí | Puede resolverse mostrando el slug ya generado para una cuenta existente, sin modificar el flujo público de reservas. |
| Negociable | Sí | La necesidad de encontrar y compartir la URL está acordada; la ubicación, el control y la confirmación visual son negociables. |
| Valiosa | Sí | Resuelve la consulta principal de los profesionales nuevos y permite comenzar a recibir reservas. |
| Estimable | No | No se definieron la ubicación de la URL, la interacción de copia ni el comportamiento ante futuros cambios de nombre o dominio. |
| Pequeña | Sí | Se concentra en exponer y copiar un dato existente dentro de la experiencia autenticada. |
| Testeable | No | La composición y unicidad son verificables, pero no puede validarse que la URL sea localizable o copiable hasta acordar la interacción esperada. |

## Criterios de Aceptación (Gherkin)

### Escenario 1: Consulta de la URL desde la experiencia autenticada

**Given** que el profesional tiene una sesión activa y su cuenta posee un slug público

**When** accede a la experiencia autenticada

**Then** puede localizar su URL pública sin intervención de soporte

**And** la URL mostrada corresponde a su propia cuenta

### Escenario 2: Composición de la URL con el dominio vigente

**Given** que la cuenta profesional tiene asignado un slug

**When** el sistema presenta su URL pública

**Then** la compone como `https://cita-ai.vercel.app/` seguida por el slug del profesional

### Escenario 3: Generación del slug a partir del nombre

**Given** que el nombre del profesional no produce una colisión con otro slug

**When** el sistema genera su URL pública

**Then** convierte el nombre a minúsculas y elimina los acentos

**And** reemplaza los espacios por guiones para formar el slug

### Escenario 4: Resolución de una colisión de slug

**Given** que ya existe en la plataforma un slug generado a partir del mismo nombre

**When** el sistema genera la URL del nuevo profesional

**Then** agrega al slug un sufijo numérico incremental que no esté utilizado

**And** la URL resultante es única en toda la plataforma

### Escenario 5: Copia directa de la URL pública

**Given** que el profesional está visualizando su URL pública

**When** ejecuta la acción de copiar

**Then** el sistema copia la URL completa

**And** la URL copiada coincide exactamente con la que se muestra

### Escenario 6: Disponibilidad del enlace durante la activación

**Given** que el profesional inicia el proceso de registro

**When** completa los pasos necesarios para activar su cuenta

**Then** puede localizar su enlace de reservas funcionando antes de que transcurran 5 minutos desde el inicio del registro

## Notas de QA

* Probar nombres con mayúsculas, acentos y varios espacios, y verificar la URL completa resultante.
* Preparar dos cuentas sintéticas con el mismo nombre para comprobar el sufijo incremental sin utilizar datos de profesionales reales.
* Comprobar que la URL mostrada y la copiada pertenecen al profesional autenticado y no a otra cuenta.
* Verificar la promesa de menos de 5 minutos desde el inicio del registro hasta que el enlace pueda localizarse y utilizarse.
* No crear cuentas ni modificar datos en producción durante este refinamiento; actualmente no existe un entorno de prueba confirmado.
* La implementación continúa `Sin verificar`; los reportes y observaciones documentan que la URL no estaba expuesta, pero no confirman el estado actual.

## Inspección Shift-Left

**Resultado:** Bloqueante

**Reporte:** `.context/testing/inspections/inspeccion-CAQ-6.md`

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| El slug se genera en minúsculas, sin acentos y con espacios reemplazados por guiones | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.4 |
| Las colisiones se resuelven con un sufijo numérico incremental y el slug es único en toda la plataforma | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 3.4 |
| El dominio vigente de las páginas públicas es `https://cita-ai.vercel.app/` | `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · La dirección, 21/05/2026 |
| El profesional necesita encontrar el enlace para compartirlo con sus clientes | `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · Registro y acceso; `.context/Confluence-corporativo/documentacion para QA/transcripcion-reunion-2026-05-19.md` · 00:01:17–00:02:20 |
| El enlace de reservas debe funcionar en menos de 5 minutos desde el inicio del registro | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · sección 10 |
| La URL no se encontró en dashboard, disponibilidad, clientes ni navegación | **Observado** — producción, 30/08/2026. Evidencia: `.context/architecture/prd.md` · Feature 1, User Journeys y Fuentes |
| Ofrecer una acción directa para copiar la URL completa | **Hipótesis** — la necesidad de compartir está documentada, pero no se acordó el control de interfaz |

## Contradicciones detectadas

* La especificación funcional utiliza `cita.ai/{slug}`, pero la nota de ambientes del 21/05/2026 establece que el dominio configurado y utilizado por los usuarios es `https://cita-ai.vercel.app/`. Se toma la fuente más reciente para componer la URL vigente.
* La especificación indica que la URL se genera durante el registro; soporte, notas técnicas y la observación de producción documentan que no se muestra en la experiencia autenticada. Se conserva la generación como comportamiento esperado y la exposición como brecha pendiente de verificar.

## Preguntas abiertas

* ¿En qué pantalla y sección de la experiencia autenticada debe mostrarse la URL pública?
* ¿La acción para compartir será un botón de copia, el enlace seleccionable, una acción nativa de compartir o una combinación?
* ¿Qué confirmación visual debe mostrarse después de copiar la URL?
* ¿El profesional puede personalizar su slug? Si cambia su nombre o slug, ¿la URL anterior redirige, deja de funcionar o permanece como alias?
* ¿Cuándo se migrará el dominio público desde `cita-ai.vercel.app` a `cita.ai` y cómo se conservarán los enlaces compartidos previamente?
* ¿Qué debe mostrar la URL pública antes de que el profesional configure disponibilidad?
