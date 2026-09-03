# Reporte de Inspección de Requisitos: Recuperación de contraseña

**Historia:** CAQ-5
**Fecha:** 03/09/2026
**Estado de sincronización:** Sincronizado con Jira

## 1. Defectos Encontrados

| ID | Tipo | Descripción del Defecto | Sugerencia de Corrección |
| :--- | :--- | :--- | :--- |
| CAQ-5-D1 | Completitud | No se define la política de la contraseña nueva. | Confirmar si reutiliza exactamente las reglas de registro. |
| CAQ-5-D2 | Caso borde | Faltan mensajes para token inválido, vencido, usado o sustituido. | Definir resultado verificable para cada partición. |
| CAQ-5-D3 | Seguridad | No se definen límites de solicitudes ni invalidación de enlaces anteriores. | Acordar rate limit, vigencia y precedencia de tokens. |

## 2. Versión Corregida de la Historia

Como profesional, quiero recuperar mi acceso mediante un token de un solo uso y una respuesta que no revele si mi correo existe. Se conservan vigencia de una hora y respuesta no enumerativa; política de contraseña, mensajes, rate limit y sesión posterior quedan `Pendiente`.

## 3. Valoración de Calidad

* **Estado:** Requiere Cambios
* **Riesgo:** Alto

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Flujo y vacíos inspeccionados | `.context/PBI/epics/EPIC-CAQ-2-cuenta-y-activacion-del-profesional/stories/STORY-CAQ-5-recuperacion-de-contrasena/story.md` |
| Token de una hora y no enumeración | `.context/architecture/prd.md` · Feature 1 |

## Contradicciones detectadas

* Ninguna detectada.

## Preguntas abiertas

* ¿Qué política cumple la nueva contraseña y qué ocurre con tokens anteriores?
* ¿Qué límites, mensajes y sesión posterior corresponden al flujo?
