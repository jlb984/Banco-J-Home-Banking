# Banco X Sistema Home Banking QA

> **Transforma tu perfil de QA tradicional a QA Augmented dominando LLMs, Context Engineering y Protocolos MCP.**

![QA AI Status](https://img.shields.io/badge/Status-Active-success)
![Focus](https://img.shields.io/badge/Focus-Shift%20Left%20%26%20Exploratory-blue)
![LLM](https://img.shields.io/badge/LLM-Copilot-orange)


---

## 📂 Estructura del Repositorio

Este proyecto está diseñado para ser tu **"Laboratorio de QA"**.

| Carpeta | Descripción |
| :--- | :--- |
| **`.prompts/`** | 🧠 **El Cerebro:** Librería de prompts de ingeniería listos para usar en cada fase (F1 a F7). |
| **`.context/`** | 🗂️ **La Memoria:** Aquí se guardan los outputs de la IA (PRDs, Planes de Prueba, Bugs). Viene vacía para que tú la llenes. |
| **`.guides/`** | 📚 **El Manual:** Guías técnicas para instalar CLIs, trabajar con Git y conectar LLMs (ver abajo). |

---

## 📚 Las Guías

| Guía | Para qué |
| :--- | :--- |
| [Inicio y setup](.guides/guia-inicio-setup.md) | Instalar todo desde cero: VS Code, terminal, Node.js y Git. **Empieza por aquí.** |
| [Git — básico](.guides/Git/git-basico.md) | Los comandos del día a día: clonar, guardar cambios, subir y bajar. |
| [Git — flujo de trabajo](.guides/Git/git-workflow.md) | El ciclo de una tarea de principio a fin y cómo escribir buenos mensajes. |
| [Git — trabajo en equipo](.guides/Git/git-colaboracion.md) | Ramas, Pull Requests, revisión entre pares y por qué `main` está protegida. |
| [`.guides/LLMs/`](.guides/LLMs/) | Instalar y configurar el asistente de IA que elijas. |
| [`.guides/mcps/`](.guides/mcps/) | Conectar herramientas por MCP: Jira, bases de datos, navegador, Postman. |
| [`.guides/postman/`](.guides/postman/) | Preparar Postman para las pruebas de API. |

> La guía de **trabajo en equipo** es la que más se saltea y la que más cuesta después. Aquí
> el repositorio no guarda código: guarda documentos, y un documento equivocado se ve igual
> que uno correcto. La revisión de otra persona es el único control que existe.

---

## 🚀 Cómo empezar

Este repositorio es una **Plantilla (Template)**. No debes trabajar directamente sobre él, sino crear tu propia copia.

### Opción A: Usar como Plantilla (Recomendado)
1.  Haz clic en el botón verde **"Use this template"** (arriba a la derecha en GitHub) -> **"Create a new repository"**.
2.  Dale un nombre a tu proyecto (ej: `mi-proyecto-qa-ia`).
3.  Clona **TU** nuevo repositorio en tu máquina:
    ```bash
    git clone https://github.com/TU-USUARIO/mi-proyecto-qa-ia.git
    cd mi-proyecto-qa-ia
    ```

### Opción B: Clonado Manual
Si prefieres clonarlo manualmente, recuerda cambiar el origen para no intentar subir cambios a este repositorio base:

```bash
# 1. Clona este repo
git clone https://github.com/Ecosistemas-QA/curso-QA-AI-Augmented.git
cd curso-QA-AI-Augmented

# 2. Elimina el vínculo con el origen
git remote remove origin

# 3. Crea tu propio repo vacío en GitHub y conéctalo
git remote add origin https://github.com/TU-USUARIO/tu-repo-nuevo.git
git push -u origin main
```

### 2. Elige tu Motor de IA
Ve a la carpeta `.guides/LLMs/` y sigue la guía de instalación para tu asistente favorito:
**Las tres del curso** — elegí una:

*   [Anthropic — Claude Code](.guides/LLMs/claudeCode/claude-Code-CLI-config.md)
*   [OpenAI — Codex](.guides/LLMs/openAI/openai-cli-config.md)
*   [Google — Antigravity CLI (`agy`)](.guides/LLMs/antigravity/instalacion-antigravity-cli.md) (reemplaza a Gemini CLI, retirada en junio de 2026)

**Alternativa para entornos corporativos** — solo si tu empresa bloquea las tres de
arriba, algo habitual en bancos y aseguradoras:

*   [GitHub Copilot CLI](.guides/LLMs/copilot/copilot-cli-config.md) (terminal)
*   [GitHub Copilot en VS Code — modo agente](.guides/LLMs/copilot/copilot-vscode-agente.md) (sin instalar nada, si ya tenés VS Code y Copilot)

### 3. Ejecuta tu primer Prompt
Abre el archivo `.prompts/1-Constitucion/business-model.md`, copia el contenido y pégalo en tu chat con la IA. ¡Mira cómo genera tu estrategia de negocio!

---

## 🎓 Programa del Curso (Las 7 Fases)

El flujo de trabajo sigue un ciclo de vida de desarrollo de software moderno:

1.  **Constitución:** Definición de Modelo de Negocio y Mercado.
2.  **Arquitectura:** Generación de PRD y Diseño Técnico.
3.  **Infraestructura:** Estrategia de Entornos y Datos de Prueba.
4.  **Especificaciones:** Creación de Backlog y User Stories (BDD).
5.  **Shift-Left Testing:** Inspección de requisitos y Análisis de Riesgos.
6.  **Testing Exploratorio:** Ejecución de pruebas en UI, API y DB ("La Trifuerza").
7.  **Documentación:** Generación de Casos de Prueba y Reportes de Cierre.

---

## 🛠️ Requisitos del Alumno

*   **Rol:** QA Manual, Analista QA o Tester.
*   **Conocimientos:** Conceptos básicos de testing (ISTQB foundation es un plus).
*   **Herramientas:**
    *   Una terminal moderna (Recomendamos **Warp**).
    *   Git instalado.
    *   Cuenta en GitHub.
    *   Acceso a un LLM (Gemini, ChatGPT o Claude).

---

## 🤝 Contribución

Este es un repositorio educativo vivo. Si encuentras un error en un prompt o quieres mejorar una guía:
1.  Crea una rama (`git checkout -b fix/mi-mejora`).
2.  Haz tus cambios.
3.  Envía un Pull Request.

---

**© 2026 Ecosistemas QA.** *QA Augmented methodology.*
