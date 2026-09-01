# Estrategia de Datos de Prueba: Cita AI

## 1. Fuentes de Datos

- **Estado vigente confirmado:** no hay entorno de prueba activo documentado; las acciones conocidas se ejecutan en producción.
- **Estado histórico de UAT:** se refrescaba desde producción. Un script sustituía nombre/email en `clients`, pero `professionals` conservaba nombre y email reales para no alterar slugs.
- **Declaración funcional contradictoria:** la especificación afirma que UAT utiliza datos ficticios generados para pruebas.
- **Capacidad faltante:** no existen seed, factories, migraciones versionadas ni reset documentados.

Por seguridad, hasta que el equipo confirme un ambiente aislado, no debe considerarse que exista una fuente válida de datos para pruebas mutantes.

## 2. Gestión de Usuarios de Prueba

| Rol | Usuario (Email/ID) | Contraseña (Referencia a Vault/Env) | Propósito |
| :--- | :--- | :--- | :--- |
| Profesional/Admin | `usuario.prueba.1@mailinator.com` | Referencia segura pendiente; no documentar el valor | Exploración de dashboard, disponibilidad y clientes |
| Cliente final | Datos sintéticos por ejecución | No aplica: no tiene cuenta | Reserva y cancelación pública |
| Profesional al límite | Fixture con 10 clientes únicos | Referencia segura por definir | Validar cliente número 11 y carga manual |

- Existe una cuenta de prueba confirmada con rol profesional. Su reutilización no convierte producción en un entorno seguro para pruebas mutantes.
- La cuenta de Fernando contiene información real y está expresamente excluida.
- Direcciones descartables solo son aceptables en un entorno autorizado; en producción igualmente crean datos y correos reales.

## 3. Generación de Datos Sintéticos

- **Herramientas actuales:** ninguna documentada.
- **Estrategia recomendada:** seed idempotente y factories versionadas para profesionales, disponibilidad, bloqueos, clientes y turnos. Esta es una hipótesis de solución, no capacidad existente.
- **Identificación:** cada ejecución debe usar un prefijo o `run_id` trazable para limpiar únicamente sus propios datos.
- **Escenarios mínimos:** agenda vacía; duraciones 45/50/60; bloques solapados; 0/9/10/11 clientes; turnos `confirmed|cancelled`; cancelación futura/pasada; Argentina/México/Chile; carrera por el mismo slot; quien reserva para otra persona.
- **Volumen:** no definir carga masiva hasta acordar capacidad y disponer de ambiente aislado.

## 4. Privacidad y Seguridad (PII)

- **Política:** usar datos sintéticos por defecto; prohibir copias de producción salvo excepción aprobada, documentada y anonimizada antes de exponerla a QA.
- **PII identificada:** nombres y emails de `professionals` y `clients`; relaciones de `appointments` y slugs pueden permitir reidentificación.
- **Anonimización histórica:** parcial. Solo se documentó reemplazo de nombre/email en `clients`; `professionals` quedó intacta y no se acreditó tratamiento de turnos, Auth, logs, backups ni correo.
- **Criterio de aceptación de anonimización:** irreversibilidad razonable, consistencia referencial y verificación automatizada de que no queden dominios, nombres o identificadores reales.
- **Credenciales:** nunca incluir contraseñas, tokens, service role ni contenido de `.env` en tickets, evidencias o commits.

**Riesgo PII detectado:** alto. Hubo una copia parcial de producción y el único entorno vigente confirmado es producción.

## 5. Limpieza y Reset (Teardown)

- **Estado actual:** no hay teardown, seed base, backup propio ni rollback de datos documentados.
- **Baseline observado de la cuenta de prueba (30/08/2026):** 0 citas próximas, 0 clientes, duración 60 minutos, sin bloqueos y todos los días no disponibles. Es una fotografía temporal, no un seed garantizado.
- **Restricción inmediata:** no ejecutar en producción escenarios que creen cuentas, clientes, reservas, cancelaciones o correos.
- **Objetivo recomendado:** restaurar un baseline sintético reproducible; limpiar por `run_id`; proteger fixtures compartidas; verificar conteos y relaciones después de cada suite.
- **Fallo de prueba:** poner en cuarentena la ejecución y conservar evidencia mínima; no realizar borrados amplios ni manuales sin identificar exactamente los registros creados.
- **Responsabilidad:** debe asignarse un dueño del reset y documentarse quién puede restaurar schema/datos.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Copia de producción, anonimización parcial y ausencia de seed/migraciones | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Ambientes, datos de UAT y deploy |
| Declaración de datos ficticios en UAT | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · Ambientes y datos de prueba |
| Producción única, datos persistentes y correos reales | `.context/Confluence-corporativo/documentacion para QA/nota-ambientes-y-accesos.md` · Lo del ambiente de UAT y Cómo entrar |
| Cuenta de Fernando excluida | `.context/Confluence-corporativo/documentacion para QA/hilo-mail-alcance-qa.md` · mail de Diego |
| Cuenta de prueba profesional y baseline visible | **Observado** — producción, 30/08/2026 mediante Playwright; no se crearon ni modificaron datos |
| Seed, factories, `run_id` y criterios de anonimización | **Hipótesis/recomendación** — no están implementados ni acordados |

## Contradicciones detectadas

- La especificación afirma datos ficticios; las notas técnicas describen copia productiva con anonimización parcial; la nota posterior afirma que UAT ya no se usa. Se prioriza el estado más reciente y se conserva el antecedente como riesgo PII.
- Las notas técnicas presentan UAT como separado, pero el correo de arranque QA advierte que todo queda y no puede revertirse. No se asume ningún reset disponible.

## Preguntas abiertas

- ¿Tenemos acceso directo a alguna base no productiva? ¿Con qué rol, auditoría y restricciones?
- ¿El proyecto UAT todavía existe y contiene PII o backups derivados de producción?
- ¿Qué datos permanecen en Supabase Auth, logs, backups y Resend fuera de las cinco tablas?
- ¿Quién aprobará y mantendrá seed, factories, usuarios fijos y teardown?
- ¿Cuál es la política de retención y eliminación de datos de prueba?
- ¿Cómo se interceptarán correos para evitar envíos externos durante pruebas?
- ¿Quién custodiará la cuenta profesional de prueba y dónde se almacenará su contraseña fuera de la conversación y del repositorio?

## Próximo paso

Continuar con `.prompts/4-Especificaciones (Backlog)/pbi-product-backlog.md`.
