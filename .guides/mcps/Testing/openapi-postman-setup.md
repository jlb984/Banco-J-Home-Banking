# Guía de Configuración: OpenAPI/Postman MCP

## 📌 Descripción
Para probar APIs, las IAs necesitan entender "cómo hablar" con ellas. Aunque no existe un "Postman MCP" oficial único, el estándar de la industria es **OpenAPI (Swagger)**.

Esta guía te enseña a conectar tu IA a cualquier API utilizando una especificación OpenAPI, la cual puedes exportar fácilmente desde Postman.

**Paquete Recomendado:** `@modelcontextprotocol/server-openapi`

## 🛠️ Preparación (Desde Postman)

Antes de configurar el MCP, necesitas el "mapa" de tu API.

1.  Abre **Postman**.
2.  Ve a tu Colección de API.
3.  Haz clic en los tres puntos `...` -> **Export**.
4.  Selecciona el formato **OpenAPI 3.0 (JSON)** o **YAML**.
5.  Guarda el archivo como `mi-api.json` en la carpeta de tu proyecto.

## ⚙️ Configuración del MCP

Configura el servidor para que "lea" ese archivo y aprenda los endpoints.

```json
"mi-api": {
  "command": "npx",
  "args": [
    "-y",
    "@modelcontextprotocol/server-openapi",
    "C:\\Ruta\\a\\tu\\proyecto\\mi-api.json"
  ]
}
```

*Nota: Puedes tener múltiples entradas para diferentes APIs (ej: "api-pagos", "api-usuarios").*

## 🚀 Uso en el Curso (Fase 6)

Una vez conectado, la IA no "adivinará" los endpoints; los **sabrá**.

**Prompt:**
> "Consulta el endpoint `GET /users/{id}` de la API que configuraste para el usuario 123 y valida si la respuesta cumple con el esquema."

**Ventajas sobre usar `curl` suelto:**
*   La IA conoce los tipos de datos esperados.
*   Sabe qué parámetros son obligatorios.
*   Entiende las descripciones de los errores documentados.

## 🧪 Verificación

Pídele a la IA:
> "Lista las operaciones disponibles en la API que acabo de configurar."

Debería responderte con un resumen de los endpoints (GET, POST, PUT) que definiste en tu archivo OpenAPI/Postman.
