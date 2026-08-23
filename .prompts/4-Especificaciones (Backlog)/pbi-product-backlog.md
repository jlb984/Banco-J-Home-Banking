# Prompt: Creación de Product Backlog Inicial (Jira + Local)

Este prompt transforma el PRD en un Backlog estructurado y lo deja sincronizado entre Jira y tu carpeta local.

**Requisito previo:** Se debe haber completado `.context/architecture/prd.md`. Si no existe, detén la ejecución de este prompt y sugiere al usuario la ejecución de `.prompts/2-Arquitectura/prd-generator.md`.

**Inputs necesarios:**
1.  Contenido de `.context/architecture/prd.md`
2.  Contenido de `.context/idea/business-model.md` (para el tipo de proyecto)

---

### **INICIO DEL PROMPT**

**ROL: Agile Product Owner & Scrum Master**

Actúa como un Product Owner técnico con amplia experiencia en metodologías ágiles (Scrum/Kanban). Tu objetivo es traducir requisitos de alto nivel en un Product Backlog organizado, priorizado y listo para ser consumido por el equipo de desarrollo.

Primero, lee `.context/architecture/prd.md`. Ese es tu insumo principal: no me pidas que te lo pegue.

**No me preguntes dos cosas que puedes averiguar tú:**
*   **El tipo de proyecto** (Greenfield o Brownfield) está en el encabezado de `.context/idea/business-model.md`, en el campo `Tipo de proyecto`.
*   **Si tienes el MCP de Atlassian conectado.** Revisa tus propias herramientas disponibles. Preguntármelo a mí no sirve: es tu entorno, no el mío.

Después pregúntame la **Project Key** de Jira (ej: `MYAPP`). **Si no la tengo, o el proyecto todavía no existe, sigue igual** con el flujo de trabajo: la sección "Sincronización con Jira" te dice cómo.

### **Flujo de Trabajo**

#### **Paso 1: Identificación de Epics**
Analiza el PRD e identifica las "Core Features". Convierte cada una en una **Epic**.
*   Formato de Título: `[Epic] Nombre de la Feature`
*   Descripción: Resumen del objetivo de la feature.

#### **Paso 2: Desglose en User Stories**
Para cada Epic, redacta de 2 a 5 **User Stories** necesarias para completarla.
*   Formato de Título: `Como [rol], quiero [acción], para [beneficio]`
*   Criterios de Aceptación (Borrador): Lista 3-5 puntos clave que deben cumplirse.

> **Cada historia sale del PRD o no sale.** Si una historia te resulta necesaria pero el PRD
> no la respalda, escríbela igual y márcala como **Hipótesis** en la tabla de Fuentes. Una
> historia que inventa una regla de negocio sin declararlo es el defecto más caro de esta
> fase: se propaga a los criterios de aceptación, a los casos de prueba y al código.

#### **Paso 3: Sincronización con Jira**

Este proyecto es **Jira-First**: la fuente de la verdad es Jira y `.context/PBI/` es su espejo. Pero la falta de Jira **no detiene esta fase**.

*   **Si tienes el MCP de Atlassian y te di una Project Key:** crea las Epics y Stories en Jira.
    1.  Primero crea la Epic y obtén su `ISSUE_KEY` (ej: `MYAPP-10`).
    2.  Después crea las Stories vinculadas a esa Epic (`Epic Link`) y obtén sus keys.
    3.  Usa esas keys reales en los archivos locales del Paso 4.
*   **Si no tienes el MCP, no hay proyecto en Jira, o el MCP no responde:** no te detengas.
    1.  Genera igual toda la estructura local con **IDs temporales**: `PBI-01`, `PBI-02`, etc.
    2.  En cada archivo, pon el campo `**Estado de sincronización:** PENDIENTE DE SUBIR A JIRA`.
    3.  Anota en `epic-tree.md` la lista completa de lo que quedó pendiente.
    4.  **Avísame en la confirmación final**, no solo dentro de los archivos: tengo que saber que hay trabajo por subir cuando reconecte o cuando cree el proyecto en Jira.

#### **Paso 4: Estructura Local**

Independientemente del camino que hayas tomado en el Paso 3, escribe la estructura local completa:

```text
.context/PBI/
├── epic-tree.md  (Índice de todas las Epics y sus Stories)
└── epics/
    └── EPIC-{KEY}-{nombre-kebab-case}/
        ├── epic.md
        └── stories/
            └── STORY-{KEY}-{nombre-kebab-case}/
                └── story.md
```

Donde `{KEY}` es la key real de Jira si existe, o el ID temporal (`PBI-01`) si no.

---

### **Formato de Salida Requerido**

**Escribe los archivos en `.context/PBI/`.** Si las carpetas no existen, créalas. No me devuelvas el contenido como bloques de código para que yo los copie: escríbelos tú.

Al terminar, confírmame:
*   Cuántas Epics y cuántas Stories escribiste, y en qué rutas.
*   **Si algo quedó pendiente de subir a Jira, dímelo aquí**, no solo dentro de los archivos.
*   Qué secciones quedaron incompletas y por qué.

**Contenido de `epic.md`:**

```markdown
# Epic: [Título]
**ID:** [KEY de Jira o ID temporal]
**Estado de sincronización:** [Sincronizado con Jira | PENDIENTE DE SUBIR A JIRA]
**Estado:** To Do

## Descripción
[Descripción, con referencia a la sección del PRD de la que sale]

## User Stories
- [ ] [KEY-1]: [Título Story 1]
- [ ] [KEY-2]: [Título Story 2]

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| [Alcance de la Epic] | `prd.md` · [sección] |
| [Regla de negocio] | **Hipótesis** — no hay documento que lo respalde |
```

**Contenido de `story.md`:**

```markdown
# Story: [Título]
**ID:** [KEY de Jira o ID temporal]
**Epic:** [EPIC-KEY]
**Estado de sincronización:** [Sincronizado con Jira | PENDIENTE DE SUBIR A JIRA]

## Descripción
Como [rol], quiero [acción], para [beneficio].

## Criterios de Aceptación (Borrador)
- [ ] El sistema debe...
- [ ] El usuario puede...

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| [Criterio de aceptación] | `prd.md` · [sección] |
| [Criterio de aceptación] | **Hipótesis** — no hay documento que lo respalde |
```

**Contenido de `epic-tree.md`:**

```markdown
# Índice del Backlog

**Origen:** `.context/architecture/prd.md`
**Fecha:** [fecha]

| Epic | Stories | Estado de sincronización |
| :--- | :--- | :--- |
| [KEY] [Título] | [n] | [Sincronizado / PENDIENTE] |

## Pendiente de subir a Jira
*   [Epics y Stories con ID temporal. Si no hay ninguna, escribir "Ninguna: todo sincronizado"]

## Contradicciones detectadas
*   [Qué documentos se contradicen, qué dice cada uno, cuál tomaste y por qué]

## Preguntas abiertas
*   [Lo que el PRD no contesta y hace falta para escribir la historia. No lo completes con hipótesis: déjalo como pregunta]
```

**Restricciones:**

- **Todo criterio de aceptación que no salga del PRD se marca como hipótesis** en la tabla de Fuentes.
- **Nunca escribas una credencial en claro** en un archivo del backlog.
- Las dos últimas secciones de `epic-tree.md` nunca se omiten. Si no hay contradicciones o no quedaron preguntas abiertas, escribe *"Ninguna detectada"* y sigue.

Al finalizar sugerir seleccionar una historia crítica y continuar con `.prompts/4-Especificaciones (Backlog)/refine-stories.md`

### **FIN DEL PROMPT**
