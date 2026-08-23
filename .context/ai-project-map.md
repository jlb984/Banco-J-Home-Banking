# 🗺️ AI Project Map: QA AI-Augmented Course

## 1. Misión y Propósito
Este repositorio es la base de un curso diseñado para transformar a **QA Manuales** en **QA Augmented Specialists**. El enfoque es el **Context Engineering**: usar la IA como un orquestador técnico que interactúa con herramientas de desarrollo (CLI, Git, Jira, DBs) a través de protocolos **MCP**.

## 2. Estructura de Archivos (Arquitectura de Contexto)

```text
.
├── .prompts/               # Librería de "Cerebros" (Fases F1-F7)
├── .context/               # Contexto del proyecto: todo lo que los prompts leen
│   ├── Confluence-corporativo/  # El Confluence del proyecto, simulado (ver abajo)
│   ├── idea/               # F1 - Constitución
│   ├── architecture/       # F2 - Arquitectura
│   ├── infrastructure/     # F3 - Infraestructura
│   ├── PBI/                # F4 - Especificaciones
│   └── testing/            # F5-F7 - Testing
├── .guides/                # Manuales técnicos (Git, LLMs, Setup)
├── .documents/             # Base de conocimiento teórica (READMEs humanos)
├── .gitignore              # Qué queda fuera del repositorio
├── .gitattributes          # Normalización de finales de línea
├── AGENTS.md               # Directivas de trabajo (fuente única)
├── CLAUDE.md               # Puntero a AGENTS.md
└── README.md               # Portada y guía de inicio
```

### Qué es `.context/`

Es la **base de conocimiento del proyecto**: todo archivo que los prompts puedan
necesitar para trabajar. Funciona como el RAG del repositorio — la IA lee de acá
antes de producir cualquier cosa. No es una carpeta de salidas.

De dónde viene cada archivo es secundario, y hay tres caminos, los tres legítimos:

| Origen | Ejemplo |
| :--- | :--- |
| **Documentación del proyecto** — la que ya venía escrita | `Confluence-corporativo/` |
| **Generado** — lo escribe un prompt al ejecutar una fase | El canvas de negocio de F1, las historias de usuario de F4 |
| **Bajado** — vive en una herramienta externa y se trae acá para que la IA lo lea | Historias o casos de prueba que ya están cargados en Jira y no en el repositorio |

### `Confluence-corporativo/`

Son seis archivos que **simulan las páginas que el equipo habría subido al Confluence
de la empresa**: documentación de negocio y técnica del proyecto Cita.ai —minuta de
kickoff, notas de entrevistas, especificación funcional, notas técnicas del
desarrollador, un hilo de mails de cambio de alcance y un resumen de tickets de
soporte—. Es el insumo del camino **Brownfield** de las Fases 1 a 3.

> **Por qué está simulado.** El curso trabaja sobre una instancia de **Jira Free**,
> que no incluye Confluence. Sin un Confluence real al que conectarse, la
> documentación se vuelca a archivos dentro del repositorio: es la forma de que la
> IA pueda leerla igual. El nombre de la carpeta es a propósito, para que se lea
> como lo que representa y no como una carpeta del curso.

> **Nota para la IA:** entre estos documentos hay **contradicciones y huecos
> puestos a propósito**. Son el ejercicio del curso, no defectos del material: no
> hay que corregirlos, unificarlos ni señalarlos como erratas al generar los
> entregables de cada fase.

## 3. Lógica de las Fases (The Workflow)

El curso sigue un flujo lineal y lógico donde cada paso alimenta al siguiente:

1.  **F1 - Constitución:** Define el negocio (`business-model.md`) y el mercado (`market-context.md`).
2.  **F2 - Arquitectura:** Genera el `prd-generator.md` y el `architecture-design.md` (incluye diseño de APIs y Diagramas Mermaid).
3.  **F3 - Infraestructura:** Mapea el entorno técnico. Matriz de componentes (Frontend, API, DB) y estrategia de datos.
4.  **F4 - Especificaciones:** Gestión de Backlog en Jira (Jira-First) y refinamiento BDD/Gherkin.
5.  **F5 - Shift-Left Testing:** Inspección estática de requisitos y corrección proactiva en la fuente. Análisis de Riesgos.
6.  **F6 - Testing Exploratorio:** Ejecución de la **"Trifuerza"** (UI, API, DB) asistida por MCPs (Playwright, Postman, SQL).
7.  **F7 - Documentación CPs:** Formalización de casos de prueba, cálculo de ROI de automatización y soporte para Xray.

## 4. Estándares Técnicos para la IA (System Prompting)

Todos los prompts en `.prompts/` siguen estos principios de optimización:

*   **Identidad (Role-Based):** Cada prompt inicia con un `ROL:` específico (Senior PM, Chief Architect, DevOps Lead, Test Manager, etc.).
*   **Encadenamiento (Chaining):** Al finalizar, cada prompt sugiere explícitamente el archivo del siguiente paso.
*   **Validación de Pre-requisitos:** Los prompts verifican la existencia del contexto anterior antes de ejecutar (Smart Logic).
*   **Clean Context:** Se han eliminado todas las instrucciones de "copia y pega". El flujo está diseñado para lectura de archivo directa.
*   **Enterprise Language:** Se ha eliminado el término "MVP" en favor de "Release Objetivo" o "Versión 1.0".

## 5. Configuración de Entorno y Git

*   **Terminal:** Optimizada para **Warp** (Warp AI / Blocks).
*   **Git Sync:** El repositorio local está configurado con un remoto `origin` que realiza un **Multi-Push** a dos destinos:
    1.  `https://github.com/Ecosistemas-QA/curso-QA-AI-Augmented.git`
    2.  `https://github.com/jlb984/curso-QA-AI-Augmented.git`
*   **Autenticación:** Uso de **Personal Access Tokens (PAT)** inyectados en las URLs de los remotos para evitar conflictos de identidad.

## 6. Estado Actual del Proyecto (Agosto 2026)

*   **Prompts:** Las siete fases están escritas, refinadas y commiteadas.
*   **Material del proyecto de práctica:** Cargada la documentación heredada de **Cita.ai**
    en `.context/Confluence-corporativo/` (seis archivos). El resto de `.context/` arranca
    vacío a propósito: se va poblando a medida que avanzan las fases.
*   **Asistentes documentados:** Claude Code, Antigravity, Codex/OpenAI, Copilot y Gemini
    en `.guides/LLMs/`.
*   **Encadenamiento:** las siete fases corren enlazadas de punta a punta. Cada prompt
    escribe su entregable en `.context/` y nombra el siguiente.
