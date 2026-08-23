# Guía de Configuración: SQLite MCP Server

## 📌 Descripción
SQLite es una base de datos ligera que vive en un solo archivo (`.db` o `.sqlite`). Es perfecta para prácticas de curso, aplicaciones móviles o entornos de desarrollo donde no quieres configurar un servidor completo.

**Ideal para:**
*   Analizar bases de datos locales.
*   Practicar SQL sin internet.
*   Validar datos de apps móviles (Android/iOS exportan a SQLite).

## 🛠️ Instalación

Abre tu terminal (Warp) y ejecuta:

```bash
npm install -g @modelcontextprotocol/server-sqlite
```

## ⚙️ Configuración

Agrega esto a tu archivo de configuración MCP (`claude_config.json` o similar).

### Estructura del Comando
```json
"sqlite": {
  "command": "npx",
  "args": [
    "-y",
    "@modelcontextprotocol/server-sqlite",
    "C:\\Ruta\\Completa\\a\\tu\\archivo.db"
  ]
}
```

*Nota: En Windows, recuerda usar doble barra invertida `\\` en las rutas.*

## 🧪 Caso de Uso para QA

Imagina que estás probando una app móvil y encuentras un bug.
1.  Extraes el archivo de base de datos del dispositivo (`app_data.db`).
2.  Configuras este MCP apuntando a ese archivo.
3.  Le dices a la IA:
    > "Analiza la tabla 'usuarios' en la base de datos sqlite y dime si el usuario 'test' se guardó con el flag 'is_active' en true."

¡Es una forma potentísima de hacer **White Box Testing** sin saber SQL avanzado!
