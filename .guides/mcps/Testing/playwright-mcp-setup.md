# Guía de Configuración: Playwright MCP (Testing UI)

## 📌 Descripción
El servidor MCP de Playwright le da "ojos y manos" a tu IA. Le permite navegar por sitios web reales, hacer clic en botones, llenar formularios y tomar capturas de pantalla. Es la herramienta principal para la **Fase 6: Testing Exploratorio**.

**Paquete:** `@modelcontextprotocol/server-playwright` (o variante comunitaria `mcp-server-playwright`).

## 🛠️ Instalación

Abre tu terminal (Warp) y ejecuta:

```bash
npm install -g @modelcontextprotocol/server-playwright
# Instalar los navegadores requeridos
npx playwright install chromium
```

## ⚙️ Configuración

Agrega esto a tu archivo JSON de configuración MCP.

```json
"playwright": {
  "command": "npx",
  "args": [
    "-y",
    "@modelcontextprotocol/server-playwright"
  ]
}
```

## 🚀 Uso en el Curso

Este MCP expone herramientas como:
*   `navigate(url)`: Ir a una página.
*   `click(selector)`: Hacer clic en un elemento.
*   `fill(selector, value)`: Escribir texto.
*   `screenshot()`: Tomar una foto de la pantalla actual.

**Ejemplo de Prompt:**
> "Navega a `https://the-internet.herokuapp.com/login`, ingresa el usuario 'tomsmith' y la contraseña 'SuperSecretPassword!', haz clic en Login y dime si aparece el mensaje de éxito."

## 🔒 Seguridad y Sandbox

*   Por defecto, la IA ejecuta esto en tu máquina local.
*   La ventana del navegador puede no ser visible (modo *headless*).
*   **Advertencia:** No le pidas a la IA que navegue a sitios maliciosos o que realice acciones destructivas en cuentas de producción reales.

## 🧪 Verificación

Pídele a la IA:
> "Navega a google.com y dime cuál es el título de la página."
