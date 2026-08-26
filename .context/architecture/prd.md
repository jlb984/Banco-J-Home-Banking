# Product Requirement Document (PRD): Cita.ai

## 1. Introducción y Objetivos
*   **Visión:** Cita.ai busca eliminar el tiempo administrativo perdido por los profesionales independientes al coordinar citas mediante mensajería. Ofrece una plataforma de auto-reserva con "fricción cero" para el cliente final (sin registro) y "simplicidad radical" para el profesional (puesta en marcha en <5 minutos). Actualmente opera bajo un modelo Freemium limitado a 10 clientes.
*   **Alcance del Release:** 
    *   *Incluido:* Gestión de disponibilidad, auto-reserva, cancelación mutua, notificaciones por correo (reservas/cancelaciones), modelo Freemium (límite).
    *   *Excluido:* Integración de pagos, múltiples profesionales por cuenta, sincronización con Google Calendar, servicios con diferentes duraciones/precios, y **temporalmente excluidos los recordatorios del día anterior** (por restricciones técnicas actuales).

## 2. User Personas
*   **Profesional (Admin):** Individuo o microempresa de 1 a 3 personas cuyo modelo de negocio depende de cobrar por su tiempo (ej. psicólogos, entrenadores). Necesita una solución que funcione sola y no exija configuraciones complejas. Tolerancia nula a la fricción administrativa.
*   **Cliente final:** Persona que busca consumir un servicio del profesional. Espera una experiencia 100% fluida, online y rápida. No desea crear una cuenta ni recordar otra contraseña simplemente para solicitar una cita.

## 3. Funcionalidades Principales (Core Features)

### Feature 1: Gestión de Agenda y Disponibilidad
*   **Descripción:** El profesional configura un horario recurrente semanal (ej. Lun-Vie, 9:00 a 18:00) y la duración estándar de sus turnos (ej. 45 min). Puede añadir bloqueos puntuales (vacaciones, turnos personales).
*   **Valor para el usuario:** Digitaliza la agenda y automatiza la oferta de horarios reales al público, evitando solapamientos involuntarios.
*   **Criterios de éxito:** El profesional logra configurar su agenda y obtener su URL pública compartible en menos de 5 minutos desde su registro.

### Feature 2: Portal de Auto-reserva Público
*   **Descripción:** Interfaz donde el cliente visualiza la disponibilidad generada dinámicamente, selecciona un bloque y reserva introduciendo únicamente nombre y correo electrónico (validando que no se exceda el límite del plan gratuito del profesional).
*   **Valor para el usuario:** El cliente final tiene autonomía total (resolviendo la reserva en <1 minuto) y se elimina el "ping-pong" de mensajes para ambas partes.
*   **Criterios de éxito:** Más del 60% de los nuevos turnos son creados autónomamente por el cliente y no introducidos a mano por el profesional.

### Feature 3: Gestión de Cancelaciones sin Registro
*   **Descripción:** El cliente puede cancelar una cita haciendo clic en un enlace único recibido por correo, sin necesidad de iniciar sesión. El profesional puede cancelar desde su panel.
*   **Valor para el usuario:** Evita que el cliente no se presente simplemente por vergüenza o pereza de enviar un mensaje de cancelación. Libera el horario para que el profesional pueda revenderlo.
*   **Criterios de éxito:** Se notifica exitosamente a la contraparte inmediatamente después de que ocurre una cancelación.

### Feature 4: Notificaciones Transaccionales
*   **Descripción:** Envío de correos automáticos ante nuevos registros, reservas completadas, límites del plan Freemium (cliente #11) y cancelaciones.
*   **Valor para el usuario:** Mantiene informadas a ambas partes en tiempo real.
*   **Criterios de éxito:** Entregabilidad de los correos mediante Resend a las bandejas principales (evitando Spam). 

## 4. User Journeys (Flujos Clave)
*   **Flujo 1 (Onboarding Profesional):** El profesional se registra -> El sistema le genera un slug y URL pública (ej. cita.ai/slug) -> Es redirigido al panel -> Configura sus franjas horarias y duración de turno -> Copia su URL y la comparte.
*   **Flujo 2 (Reserva del Cliente):** El cliente ingresa a la URL pública -> Observa las ranuras (slots) disponibles de la semana calculadas en base a las reglas de disponibilidad -> Selecciona un horario -> Introduce nombre y correo -> Se verifica concurrencia -> Reserva confirmada -> Recibe email con link de cancelación.
*   **Flujo 3 (Cancelación del Cliente):** El cliente revisa su correo de confirmación -> Pulsa el enlace "Cancelar" -> El sistema da de baja el turno sin solicitar contraseña -> El horario vuelve a liberarse en la agenda pública -> El profesional recibe aviso por email.

## 5. Requisitos No Funcionales (NFRs)
*   **Seguridad:** 
    *   Autenticación gestionada con Supabase Auth (token expira en 15 min, refresh token 7 días).
    *   Políticas RLS (Row Level Security) estrictas, salvo en creación de citas (insert público) por no requerir sesión del cliente final.
    *   *Riesgo/Hipótesis:* La cancelación vía URL única es pública (bypass a RLS); si un atacante deduce el ID de la cita, podría cancelarla sin permisos.
*   **Rendimiento (Estado actual, no compromisos):** 
    *   Carga de página pública en < 2 segundos. Tiempos de API < 500ms (P95). Consultas DB < 100ms. *Nota: Estos valores son mediciones del equipo de desarrollo, no SLIs acordados por negocio.*
*   **Compatibilidad:** Aplicación Web (Next.js) con diseño responsivo prioritario para uso móvil, dado que gran parte de los usuarios y clientes reservan desde celulares (según pruebas mencionadas).

## 6. Riesgos y Mitigaciones
*   **Falta de recordatorios automáticos:** (El riesgo principal documentado). La mitad del valor para perfiles propensos a inasistencias es el recordatorio 24hs antes. Su ausencia actual debido a falta de *cron jobs* es un riesgo grave para la retención. **Mitigación temporal:** Monitorear el ausentismo (no-shows) de cerca, o evaluar un upgrade rápido en el plan de Vercel/terceros.
*   **Condición de carrera (Race Condition) en reservas:** La validación de superposición tiene una pequeña ventana de vulnerabilidad al no realizarse mediante una transacción atómica pura (solo un doble chequeo). **Mitigación:** Monitorizar incidentes de dobles reservas hasta migrar a una función atómica (Postgres function).
*   **Spam en correos:** El uso del dominio de prueba de Resend está enviando correos al spam. **Mitigación:** Verificar un dominio propio urgente.
*   **Zonas horarias:** Aunque se aplicó un parche reciente por cruces horarios con clientes en otros países, la arquitectura guarda fechas en local sin conversión estricta, lo que podría fallar si el profesional viaja o tiene clientes remotos de manera consistente.

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Ausencia de registro para cliente final | `01-minuta-kickoff.md` · Sección "Los dos usuarios del sistema" / `03-especificacion-funcional-v0.3.md` · Sección "2.2 Cliente final" |
| Setup de cuenta en <5 minutos | `01-minuta-kickoff.md` · Sección "Qué queremos que pase" / `02-notas-entrevistas.md` · Sección "Lo que saco de las siete" |
| 10 clientes límite del Freemium | `01-minuta-kickoff.md` · Sección "El modelo freemium" / `03-especificacion-funcional-v0.3.md` · Sección "8. Plan gratuito" |
| Stack técnico, mediciones NFR y bypass de RLS en cancelación | `04-notas-tecnicas.md` |
| Recordatorios pospuestos por falta de cron y paso a Resend | `05-hilo-mail-cambio-de-alcance.md` |
| Bug de zonas horarias y URL no visible | `06-tickets-soporte-resumen.md` |

## Contradicciones detectadas
*   **Transaccionalidad en Reservas:** La especificación funcional (`03-especificacion-funcional-v0.3.md` RN-02) exige que la revisión de disponibilidad se haga para evitar que dos clientes reserven al mismo tiempo. Sin embargo, las notas técnicas (`04-notas-tecnicas.md`) indican que esto se resolvió con un doble chequeo en código en lugar de una transacción SQL, lo que deja la ventana de error semiabierta (validado por un reporte posterior en `06-tickets-soporte-resumen.md`). *Tomo la implementación técnica actual como la realidad operativa.*
*   **Estado de los Recordatorios:** El PRD/Minuta los lista como obligatorios, pero los mails y soporte dictan que **no existen en producción**. *Tomo que no están implementados, catalogándolos como exclusión temporal y riesgo principal.*

## Preguntas abiertas
*   ¿Existen SLA/SLOs oficiales de rendimiento y disponibilidad acordados, o seguiremos basándonos en las mediciones *ad-hoc* registradas por desarrollo (ej: page load <2s)?
*   El manejo de Zonas Horarias, ¿debe reformularse desde la base para guardar todo en UTC?
*   ¿Cómo resolveremos la ausencia de *Cron Jobs* para habilitar los recordatorios del día anterior de forma definitiva (pagar plan de Vercel vs usar servicio externo)?
*   *Ofrecimiento MCP:* Actualmente Playwright está configurado. ¿Deseas que mapee y documente con capturas el "Happy Path" exacto que sigue hoy un usuario en el entorno en vivo (`cita-ai.vercel.app`), de manera de asentar con fidelidad cómo está implementada la interfaz real?
