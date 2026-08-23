# Fase 4: Especificaciones (Backlog)

## 🎯 Objetivo de la Fase
Crear y refinar las **Historias de Usuario** que guiarán el desarrollo y las pruebas. Aquí traducimos el PRD en tareas accionables.

## 🔑 Conceptos Clave

### 1. INVEST
Criterios de calidad para una User Story:
*   **I**ndependent (Independiente)
*   **N**egotiable (Negociable)
*   **V**aluable (Valiosa)
*   **E**stimable (Estimable)
*   **S**mall (Pequeña)
*   **T**estable (Testeable)

### 2. Gherkin (BDD)
Lenguaje estructurado para definir criterios de aceptación:
*   **Given:** Contexto inicial.
*   **When:** Acción del usuario.
*   **Then:** Resultado esperado.

### 3. Jira-First Workflow
La fuente de la verdad es Jira. La carpeta local `.context/PBI/` es un espejo para que la IA pueda analizar el backlog.

**Pero Jira no bloquea la fase.** Si todavía no hay proyecto en Jira, o el MCP no responde, los prompts escriben igual el backlog local con IDs temporales (`PBI-01`) y marcan cada archivo con `Estado de sincronización: PENDIENTE DE SUBIR A JIRA`. El índice `epic-tree.md` lleva la lista de lo que queda por subir. Se trabaja igual, y no se pierde el rastro de lo que falta sincronizar.

## 🛠️ Herramientas Utilizadas
*   **Prompts de IA:** `pbi-product-backlog.md`, `refine-stories.md`.
*   **Jira / Atlassian MCP:** Para gestión de tickets nativos.


## 📝 Entregables Esperados
Al finalizar esta fase, tendrás en tu carpeta `.context/PBI/`:
1.  Un **Backlog** priorizado en Jira y localmente.
2.  Historias de Usuario refinadas con **Criterios de Aceptación en Gherkin**.
