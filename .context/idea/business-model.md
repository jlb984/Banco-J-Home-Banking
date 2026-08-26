# Business Model Canvas: Cita.ai

**Tipo de proyecto:** Brownfield

## 1. Propuesta de Valor (Value Propositions)
*   **Para el profesional:** Ahorro de tiempo administrativo (mínimo 30 minutos semanales) al eliminar el "ping-pong" de mensajes. Simplicidad radical: sin configuración compleja, listo para usar en menos de 5 minutos.
*   **Para el cliente final:** Auto-reserva rápida en menos de un minuto sin necesidad de registrarse ni crear cuenta. Visibilidad inmediata de la disponibilidad real del profesional. Cancelación sencilla a través del correo.

## 2. Segmentos de Clientes (Customer Segments)
*   **Profesionales independientes y microempresas (1-3 empleados)** cuyo producto principal es su tiempo (psicólogos, entrenadores personales, estilistas, profesores particulares).
*   **Restricción actual:** Un solo profesional por agenda. Negocios con múltiples profesionales que requieren agendas separadas no están soportados actualmente.

## 3. Canales (Channels)
*   **Distribución propia del profesional:** La plataforma genera una URL pública única (ej. `cita.ai/slug`) que el profesional comparte en sus canales existentes (enlace en la bio de Instagram, estado de WhatsApp, sitio web personal). No funciona como un marketplace, la plataforma ordena a los clientes que el profesional ya atrajo.

## 4. Relación con Clientes (Customer Relationships)
*   **Self-service (Auto-servicio):** El profesional se registra y configura su disponibilidad de forma totalmente autónoma.
*   **Fricción cero para el cliente:** El cliente final realiza todo el proceso de reserva y cancelación sin interacción humana y sin barreras de registro.
*   **Automatización de comunicaciones:** Confirmaciones y avisos de cancelación automatizados vía correo electrónico (los recordatorios del día anterior están planeados pero pendientes).

## 5. Fuentes de Ingresos (Revenue Streams)
*   **Modelo Freemium:** Plan gratuito limitado a 10 clientes únicos (personas diferentes, sin límite de turnos para los mismos).
*   **Plan Pro (Futuro):** Monetización a través de una suscripción de pago (Plan Pro) para profesionales que superen los 10 clientes. Precios y características aún por definir. No se cobra comisión por reserva ni se integran pasarelas de pago.

## 6. Recursos Clave (Key Resources)
*   **Plataforma tecnológica:** Frontend y Backend (Next.js, Tailwind, Supabase para base de datos y autenticación, alojado en Vercel).
*   **Infraestructura de notificaciones:** Servicio de correos transaccionales (Resend) para la entrega de confirmaciones y cancelaciones.
*   **URL y dominios:** Sistema de generación de slugs públicos para cada profesional.

## 7. Actividades Clave (Key Activities)
*   **Desarrollo de producto:** Mantenimiento de la plataforma, resolución de bugs (ej. problemas recientes con zonas horarias).
*   **Operaciones:** Monitoreo del límite de clientes del plan gratuito para incentivar el salto al Plan Pro. 
*   **Gestión técnica:** Implementación de soluciones para trabajos en segundo plano (como los cron jobs pendientes para los recordatorios).

## 8. Socios Clave (Key Partners)
*   **Proveedores de nube e infraestructura:** Supabase (BaaS) y Vercel (Hosting).
*   **Proveedor de correo:** Resend, utilizado para el envío de correos transaccionales (anteriormente se evaluó SendGrid y Supabase Auth).
*   *(Ausencias estratégicas)*: No hay asociaciones con pasarelas de pago (Mercado Pago, Stripe) ni integraciones con Google Calendar por decisión deliberada de alcance.

## 9. Estructura de Costos (Cost Structure)
*   **Costos de infraestructura técnica:** Hospedaje en Vercel y servicios de base de datos/autenticación en Supabase.
*   **Costos de comunicación:** Volumen de envíos de correos transaccionales a través de Resend.
*   **Desarrollo y mantenimiento:** Costos de diseño, programación y soporte (aunque actualmente el equipo es interno).

## Problem Statement (Resumen)
*   Los profesionales independientes pierden múltiples horas semanales coordinando turnos de forma manual a través de chats de WhatsApp e Instagram. Este proceso ineficiente ("ping-pong" de mensajes) genera frustración, dobles reservas accidentales, pérdida de prospectos por respuestas tardías, y ausencias no avisadas de clientes.

## Fuentes
| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Simplicidad radical y canales de distribución | `01-minuta-kickoff.md` · Secciones "Cómo llega el cliente al profesional" y "Contra quién competimos" |
| Límite Freemium de 10 clientes | `01-minuta-kickoff.md` · Sección "El modelo: freemium" |
| Dolores y fricción cero del cliente (sin registro) | `02-notas-entrevistas.md` · Entrevistas 1, 2 y 4 |
| Sin pasarelas de pago ni integraciones GCalendar | `03-especificacion-funcional-v0.3.md` · Sección "1. Alcance" |
| Componentes tecnológicos (Vercel, Supabase) | `04-notas-tecnicas.md` · Sección "stack" |
| Uso de Resend y retraso en recordatorios | `05-hilo-mail-cambio-de-alcance.md` · Hilo completo |
| Necesidad latente de recordatorios | `06-tickets-soporte-resumen.md` · Sección "Recordatorios" |
| Diseño de la página de inicio/login | `https://cita-ai.vercel.app/` |

## Contradicciones detectadas
*   **Sistema de envío de correos:** El archivo `04-notas-tecnicas.md` documenta que los correos salen por el servicio transaccional de Supabase. Sin embargo, el archivo `05-hilo-mail-cambio-de-alcance.md` indica un cambio tardío a **Resend** por problemas de entregabilidad y formato. Prevaleció Resend por ser información más reciente.
*   **Recordatorios automáticos:** En `01-minuta-kickoff.md` y `03-especificacion-funcional-v0.3.md` los recordatorios del día anterior son un requisito obligatorio. No obstante, en `05-hilo-mail-cambio-de-alcance.md` se decide lanzar sin ellos por limitaciones técnicas (falta de cron en el plan de Vercel), y en los tickets de soporte (`06-tickets-soporte-resumen.md`) los usuarios reclaman activamente esta función.
*   **Manejo de reservas concurrentes:** La especificación funcional (`03-especificacion-funcional-v0.3.md`) requiere un estricto control de concurrencia. Técnicamente (`04-notas-tecnicas.md`), solo se implementó una doble verificación sin transacciones reales, lo que sumado a un bug de zonas horarias generó problemas reales de doble reserva (reportado en `06-tickets-soporte-resumen.md`).

## Preguntas abiertas
*   ¿Cuáles serán las características concretas y el precio del futuro "Plan Pro"?
*   ¿Cómo se implementarán técnicamente los recordatorios automáticos del día anterior, dada la restricción actual de trabajos programados (cron)?
*   ¿Se abordará el caso de uso donde el usuario que coordina no es el mismo que recibe el servicio (ej. madres reservando para sus hijos)?
*   ¿Existe algún plan para soportar negocios con más de un profesional que comparten cuenta o lugar físico?
*   ¿Cuándo se verificará un dominio propio en Resend para solucionar definitivamente los problemas de correos en spam?
