# Business Model Canvas: Cita AI

**Tipo de proyecto:** Brownfield

## 1. Propuesta de Valor (Value Propositions)

- Permitir que profesionales independientes publiquen su disponibilidad y que sus clientes reserven y cancelen turnos sin intercambios manuales por WhatsApp, Instagram o teléfono.
- Reducir el tiempo administrativo, los errores de agenda y la demora en responder a nuevos clientes mediante una experiencia web simple, sin instalación y pensada para configurarse en menos de cinco minutos.
- Ofrecer al cliente final disponibilidad visible, confirmación inmediata y reserva sin crear una cuenta: solo informa nombre y correo electrónico.
- Posicionarse entre la complejidad de Acuity Scheduling y el enfoque genérico de Calendly, con funciones propias de un negocio de servicios. El valor frente a los *no-shows* está incompleto mientras no exista el recordatorio previo al turno.

## 2. Segmentos de Clientes (Customer Segments)

- **Cliente que adopta y potencialmente paga:** profesionales independientes que trabajan solos, o microempresas de uno a tres integrantes cuyo ingreso depende de vender tiempo. Los rubros iniciales son psicología y terapias, entrenamiento personal, estilismo, nutrición y clases particulares.
- **Usuario del flujo público:** personas habituadas a resolver gestiones en línea, que prefieren elegir un horario y recibir confirmación sin esperar una respuesta del profesional.
- La versión actual está diseñada para un profesional y una agenda. Salones, consultorios y redes con varios profesionales expresaron interés, pero hoy quedan fuera del alcance efectivo.

## 3. Canales (Channels)

- Cada profesional comparte su URL pública con la audiencia que ya posee, principalmente mediante WhatsApp, Instagram o su sitio web. Cita AI ordena la demanda existente; no funciona como buscador ni marketplace.
- La adquisición inicial se apoya en contactos, demostraciones comerciales y un *soft launch* con 32 profesionales; no hay un canal de adquisición escalable documentado.
- La aplicación vigente opera en `https://cita-ai.vercel.app/`. La observación pública del 27/08/2026 confirmó que la raíz redirige al login y ofrece registro gratuito, pero no permitió descubrir páginas de profesionales sin conocer un slug válido.

## 4. Relación con Clientes (Customer Relationships)

- Incorporación autoservicio del profesional mediante registro, configuración de agenda y generación automática de una URL pública.
- Experiencia autoservicio del cliente final, sin cuenta ni aprobación previa: el turno nace confirmado y la cancelación se realiza desde el enlace enviado por correo.
- Comunicaciones transaccionales de bienvenida, confirmación, nueva reserva y cancelación. La casilla de soporte opera de forma reactiva y no hay monitoreo ni guardia documentados.
- El panel aplica el límite freemium y presenta una llamada a conocer el futuro Plan Pro. La dificultad actual para encontrar la URL pública debilita la promesa de activación en cinco minutos.

## 5. Fuentes de Ingresos (Revenue Streams)

- El producto no tiene ingresos documentados: todos los usuarios actuales utilizan el plan gratuito y el Plan Pro todavía no existe.
- El mecanismo previsto de conversión limita el plan gratuito a **10 clientes únicos por profesional**. Los clientes existentes pueden seguir reservando; el cliente número 11 queda bloqueado y el profesional recibe una invitación a obtener más información sobre el Plan Pro.
- La intención original era medir interés: más del 15 % de quienes alcanzaran el límite debían hacer clic en la llamada a conversión. No hay resultados documentados ni precio, medio de cobro o beneficios definidos para el plan pago.

## 6. Recursos Clave (Key Resources)

- La plataforma web, la lógica de disponibilidad y reservas, las URLs públicas, los datos de profesionales, clientes y turnos, y los flujos de correo transaccional.
- Infraestructura administrada con Next.js y Vercel para la aplicación, Supabase para autenticación y base de datos, y Resend para correos del producto.
- El conocimiento del equipo de Producto, Desarrollo, Diseño, Comercial y QA, junto con entrevistas, consultas de soporte y comportamiento observado.
- La base inicial de profesionales y sus propias audiencias, necesarias para distribuir los enlaces de reserva.

## 7. Actividades Clave (Key Activities)

- Mantener registro y acceso, configuración de disponibilidad, cálculo de horarios, reserva, cancelación, listado de clientes y aplicación del límite gratuito.
- Operar los correos transaccionales y mejorar su entregabilidad; implementar el recordatorio previo al turno para cubrir el problema de los *no-shows*.
- Documentar el comportamiento real, validar los flujos críticos y atender incidentes de concurrencia, husos horarios, permisos y seguridad.
- Incorporar profesionales, facilitar demostraciones y medir activación, retención, auto-reserva y conversión al Plan Pro.

## 8. Socios Clave (Key Partners)

- **Vercel:** alojamiento y despliegue de la aplicación.
- **Supabase:** autenticación, PostgreSQL y políticas de acceso a datos.
- **Resend:** envío de correos del producto; Supabase mantiene los correos propios de autenticación.
- Los servicios y redes donde los profesionales ya tienen audiencia —por ejemplo, WhatsApp e Instagram— son canales externos relevantes, pero no hay alianzas comerciales documentadas.

## 9. Estructura de Costos (Cost Structure)

- Infraestructura de Vercel, Supabase y Resend; un plan superior o un servicio programado sería necesario para ejecutar recordatorios automáticos.
- Desarrollo, mantenimiento, diseño, soporte, QA y documentación de un producto que hoy carece de pruebas automatizadas, monitoreo y un entorno UAT vigente.
- Adquisición y acompañamiento comercial de profesionales en un mercado con barreras técnicas bajas y costos de captación reconocidos como altos.
- Configuración de dominio, entregabilidad de correo, seguridad, respaldo de datos y escalabilidad. No existen importes ni proyecciones financieras documentadas.

## Problem Statement (Resumen)

- Los profesionales independientes que venden su tiempo coordinan turnos por canales desconectados y agendas manuales. Pierden entre media hora y cuatro horas semanales, responden fuera de horario, pueden duplicar reservas y pierden ingresos ante olvidos o cancelaciones tardías. Sus clientes, a su vez, esperan respuestas, intercambian varios mensajes y no siempre saben si la cita quedó confirmada. Cita AI busca reemplazar esa coordinación por una agenda pública de auto-reserva simple; todavía no cubre completamente los *no-shows* porque el recordatorio previo no está implementado.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Problema, segmentos iniciales, canal por URL propia, posicionamiento y modelo freemium | `01-minuta-kickoff.md` · De dónde sale la idea, A quién le vendemos, Cómo llega el cliente y El modelo |
| Entre media hora y cuatro horas semanales de coordinación; necesidad de baja fricción | `02-notas-entrevistas.md` · Entrevistas y Lo que saco de las siete |
| Alcance funcional, reserva sin cuenta, límite de 10 clientes y Plan Pro inexistente | `03-especificacion-funcional-v0.3.md` · Alcance, Perfiles de usuario y Plan gratuito y límite |
| Stack, recursos técnicos, riesgos operativos y ausencia de pruebas/monitoreo | `04-notas-tecnicas.md` · Stack, Límite del plan, Mails y Lo que no está hecho |
| Resend, recordatorio fuera del lanzamiento, 32 participantes y métricas objetivo | `05-hilo-mail-cambio-de-alcance.md` · hilo completo |
| Problemas reales de recordatorios, URL pública, límite, zonas horarias y varios profesionales | `06-tickets-soporte-resumen.md` · categorías de soporte |
| Objetivo de reconstruir y validar el comportamiento actual | `documentacion para QA/hilo-mail-alcance-qa.md` · Arranque de QA |
| URL vigente y existencia de un único entorno productivo | `documentacion para QA/nota-ambientes-y-accesos.md` · La dirección y Lo del ambiente de UAT |
| Interés comercial de una red de unos 20 profesionales y focos de soporte | `documentacion para QA/transcripcion-reunion-2026-05-19.md` · 00:00:38–00:08:26 |
| Raíz redirigida al login, propuesta “Gestión inteligente de citas y turnos” y registro gratuito | **Observación con Playwright** · `https://cita-ai.vercel.app/` y `/login`, 27/08/2026 |
| Costos monetarios, precio y composición del Plan Pro | **Hipótesis** — las categorías operativas están documentadas, pero no hay importes ni plan comercial definido |

## Contradicciones detectadas

- **Dirección y ambientes:** la especificación y las notas técnicas describen `cita.ai`, `uat.cita.ai` y dos bases; la nota del 21/05/2026 establece que el dominio nunca se configuró y solo existe producción en `cita-ai.vercel.app`. Se toma la nota más reciente y la observación actual de la redirección al login.
- **Proveedor de correo:** el *kickoff* menciona SendGrid, la especificación y las notas técnicas mencionan Supabase, y el hilo previo al lanzamiento confirma Resend para correos del producto. Se toma Resend por ser la decisión posterior; Supabase queda para autenticación.
- **Recordatorio:** el *kickoff* y la especificación lo presentan como requisito; el hilo de febrero/marzo de 2026 y la transcripción de mayo confirman que no fue implementado y continúa fuera del alcance inmediato. El resumen automático dice “próxima iteración”, pero contradice la transcripción fuente; se toma la transcripción.
- **Llamada a conversión:** aparecen “Solicitar Upgrade”, “Ver Opciones” y “Más información sobre el Plan Pro”. Se toma la última decisión explícita del hilo de correo.
- **Turnos duplicados:** el resumen automático atribuye ambos casos a husos horarios y los da por resueltos; en la transcripción Diego confirma solo uno y admite haber asumido la causa del otro. Se conserva un caso como no confirmado.

## Preguntas abiertas

- ¿Qué precio, beneficios, medio de cobro y criterio de conversión tendrá el Plan Pro?
- ¿Cuáles fueron los resultados reales de activación, retención, auto-reserva y clics en el Plan Pro tras el *soft launch*?
- ¿Cuándo se implementará el recordatorio, a qué hora se enviará y cómo se financiará la ejecución programada?
- ¿Qué debe ocurrir con los turnos existentes cuando el profesional bloquea un período?
- ¿Habrá una anticipación máxima para reservar y una ventana mínima para cancelar?
- ¿Cómo se representará a quien reserva para otra persona y cuándo se admitirán varias agendas por cuenta?
- ¿Cómo se resolverán la visibilidad de la URL pública, el dominio propio y la entregabilidad de los correos?
- ¿Está resuelto el acceso al panel después de cerrar sesión y el riesgo residual de reservas duplicadas?
- ¿Qué funciones de inteligencia artificial justifican el nombre Cita AI? No hay ninguna documentada ni observable en la superficie pública.
- ¿Cuál es el tamaño de mercado validado y cuál será el canal de adquisición escalable? El dato de USD 400 millones del *kickoff* no incluye una fuente verificable.

## Próximo paso

Continuar con `.prompts/1-Constitucion/market-context.md`.
