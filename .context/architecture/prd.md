# Product Requirement Document (PRD): Cita AI

## 1. Introducción y Objetivos

- **Visión:** permitir que profesionales independientes publiquen su disponibilidad y que sus clientes reserven o cancelen turnos sin coordinación manual por chat.
- **Tipo de proyecto:** Brownfield. El producto está en uso; este PRD reconstruye el alcance esperado y separa lo documentado, lo observado y lo pendiente.
- **Objetivos de negocio documentados:** ahorrar al profesional al menos 30 minutos semanales, lograr más de 60 % de auto-reservas y superar 40 % de retención a cuatro semanas. No hay resultados reales consolidados para confirmar estas metas.
- **Alcance funcional reconstruido:** cuenta del profesional, una agenda por cuenta, página pública, reserva sin registro del cliente, cancelación, correos transaccionales, clientes y límite gratuito de 10 clientes únicos.
- **Fuera de alcance vigente:** pagos, sincronización con calendarios externos, múltiples profesionales, múltiples servicios o precios, formularios personalizados, reportes y aplicaciones nativas.

## 2. User Personas

- **Profesional independiente:** vende su tiempo, trabaja solo y administra una agenda. Laura representa el dolor de coordinación; Carlos, el impacto de cancelaciones tardías y no-shows.
- **Cliente final digital:** quiere consultar disponibilidad, reservar y cancelar sin esperar respuestas ni crear una cuenta. Sofía es el perfil de referencia.
- **Casos no resueltos:** quien reserva para otra persona y organizaciones con varias agendas no encajan en el modelo actual.

## 3. Funcionalidades Principales (Core Features)

### Feature 1: Cuenta y activación del profesional

- **Descripción:** registro con nombre, email y contraseña; inicio de sesión, recuperación y generación de slug público único.
- **Valor para el usuario:** comenzar a recibir reservas con configuración mínima.
- **Criterios de éxito documentados:** registro válido crea cuenta y sesión; recuperación no revela si el email existe y usa token de una hora; el profesional obtiene una URL pública única.
- **Estado observado:** el usuario de prueba inicia sesión como profesional y accede a `/dashboard`. El panel muestra “Citas Hoy”, “Próxima Cita”, “Clientes Totales”, “Ingresos Mes” y “Próximas Citas”; los dos indicadores comerciales aparecen como “En desarrollo”. No se encontró la URL pública en dashboard, disponibilidad, clientes ni navegación.

### Feature 2: Agenda y disponibilidad

- **Descripción:** configurar disponibilidad semanal, una duración estándar y bloqueos puntuales; consultar y cancelar turnos.
- **Valor para el usuario:** ofrecer únicamente horarios utilizables y reducir errores de agenda.
- **Criterios de éxito documentados:** fin posterior a inicio, bloques sin solapamiento, guardado que reemplaza la configuración completa y exclusión de turnos confirmados/bloqueos al calcular slots.
- **Regla no definida:** qué ocurre con reservas existentes cuando se bloquea su período.
- **Estado observado:** `/dashboard/availability` permite elegir duración entre 15, 30, 45, 60, 90 y 120 minutos; crear bloqueos con fecha/hora inicial, fecha/hora final y motivo opcional; y activar días de domingo a sábado. La cuenta tenía 60 minutos, ningún bloqueo y todos los días desactivados. No se guardaron cambios.

### Feature 3: Página pública y auto-reserva

- **Descripción:** consultar disponibilidad por URL del profesional, seleccionar horario e informar nombre y email sin cuenta.
- **Valor para el usuario:** reservar en segundos sin intercambio de mensajes.
- **Criterios de éxito documentados:** no ofrecer pasado ni slots ocupados; revalidar disponibilidad al confirmar; conservar datos si otro cliente toma el horario; crear el turno en estado `confirmed` sin aprobación.
- **Riesgo conocido:** la doble verificación actual reduce, pero no elimina, la carrera entre reservas concurrentes.

### Feature 4: Cancelaciones y comunicaciones

- **Descripción:** cancelar desde el panel o mediante enlace único del correo; enviar bienvenida, confirmación, aviso de nueva reserva y aviso de cancelación.
- **Valor para el usuario:** mantener informadas a las partes y liberar horarios sin conversación manual.
- **Criterios de éxito documentados:** solo cancelar turnos futuros, pasar a `cancelled`, liberar el horario y notificar a quien no canceló.
- **Brecha:** el recordatorio del día anterior fue requerido y luego excluido del lanzamiento; no se considera construido.
- **Sin verificar:** no se recorrieron reserva, correos ni cancelación porque la cuenta no expone su URL pública y probarlos habría creado datos/correos en producción.

### Feature 5: Clientes y límite freemium

- **Descripción:** listar/cargar clientes y limitar el plan gratuito a 10 clientes únicos por profesional, identificados por email.
- **Valor para el negocio:** validar adopción y registrar intención de conversión.
- **Criterios de éxito documentados:** clientes existentes siguen reservando; el cliente nuevo número 11 y la carga manual quedan bloqueados; el profesional recibe aviso y acceso a información del Plan Pro.
- **Brecha:** el Plan Pro, precio, cobro y beneficios no existen como oferta definida.
- **Estado observado:** `/dashboard/clients` mostró 0 clientes y el botón “Nuevo Cliente”. Al pulsarlo no apareció formulario, diálogo ni cambio visible; no se realizó ningún alta.

## 4. User Journeys (Flujos Clave)

- **Activación documentada:** registro → sesión automática → configuración inicial → generación de URL → compartirla. La consulta/copia de esa URL en el panel es un gap.
- **Reserva documentada:** abrir URL → ver semana → elegir slot → informar nombre/email → confirmar → ver confirmación y recibir correo.
- **Conflicto de reserva:** confirmar slot → revalidar → si ya fue tomado, rechazar con mensaje, refrescar disponibilidad y conservar datos.
- **Cancelación:** abrir enlace o turno del panel → cancelar futuro → liberar slot → avisar a la otra parte.
- **Límite:** identificar cliente nuevo número 11 → rechazar reserva/carga → avisar al profesional → ofrecer información del Plan Pro.
- **Navegación observada:** el menú autenticado contiene Dashboard, Disponibilidad y Clientes. No contiene una opción visible para perfil público, configuración de cuenta o Plan Pro.

Todos los journeys autenticados y de reserva permanecen **sin verificar contra la aplicación** en este reprocesamiento, porque el único entorno confirmado es producción y no se generaron datos.

## 5. Requisitos No Funcionales (NFRs)

- **Seguridad existente documentada:** Supabase Auth, cookies `httpOnly`, middleware para dashboard, RLS y respuesta no enumerativa en recuperación.
- **Seguridad observada:** “Salir” cambió la navegación a “Iniciar Sesión/Registrarse Gratis”, pero no redirigió y las rutas `/dashboard`, `/dashboard/availability` y `/dashboard/clients` continuaron renderizando sus pantallas sin sesión. No se intentó guardar ni consultar datos sensibles después del logout.
- **Rendimiento medido, no acordado:** página pública <2 s, API p95 300–500 ms y usabilidad <3 s según notas técnicas. No son objetivos comprometidos.
- **Disponibilidad y capacidad:** no hay SLO, monitoreo ni prueba formal de concurrencia. La referencia de 100 usuarios simultáneos es una estimación técnica, no un requisito.
- **Compatibilidad:** web responsive; navegadores, versiones, resoluciones y requisitos de accesibilidad no están definidos.
- **Privacidad:** no usar PII ni credenciales reales en pruebas o documentación; hoy no existe un entorno de prueba confirmado.

## 6. Riesgos y Mitigaciones

- **No-shows sin recordatorio:** priorizar decisión e implementación programada; medir entrega y reducción de ausencias.
- **Reserva concurrente:** mover validación e inserción a una transacción atómica y cubrirla con pruebas de carrera.
- **Husos horarios:** definir zona del profesional y representación de timestamps; probar Argentina, México y Chile.
- **Acceso no revocado:** verificar el reporte de panel accesible después de logout antes de afirmar que está resuelto.
- **Pruebas en producción:** limitarse a lectura hasta disponer de ambiente aislado, seed y reset.
- **Conversión indefinida:** definir Plan Pro antes de usar el límite como mecanismo comercial.

## Fuentes

| Dato / afirmación | De dónde sale |
| :--- | :--- |
| Visión, segmentos, alcance, métricas y modelo freemium | `.context/idea/business-model.md` · secciones 1–9 y Problem Statement |
| Reglas funcionales esperadas | `.context/Confluence-corporativo/03-especificacion-funcional-v0.3.md` · secciones 3–10 |
| Implementación técnica, mediciones y brechas | `.context/Confluence-corporativo/04-notas-tecnicas.md` · Auth, slots, reserva, mails y rendimiento |
| Cambios posteriores al borrador funcional | `.context/Confluence-corporativo/05-hilo-mail-cambio-de-alcance.md` · resumen del 03/03/2026 |
| Incidentes y necesidades reales | `.context/Confluence-corporativo/06-tickets-soporte-resumen.md` · categorías de soporte |
| Login y formulario de registro visibles | **Observado** — producción, 30/08/2026. Evidencia: snapshot de Playwright de `/login`; no se enviaron formularios |
| Rol profesional, dashboard, navegación, disponibilidad y clientes | **Observado** — producción, 30/08/2026 mediante Playwright; no se modificaron datos |
| Pantallas de dashboard accesibles después de logout | **Observado** — producción, 30/08/2026 mediante Playwright; no se probaron escrituras sin sesión |
| Transacción atómica y matriz de compatibilidad | **Hipótesis/recomendación** — no son requisitos acordados |

## Contradicciones detectadas

- La especificación incluye recordatorio; el hilo de lanzamiento, soporte y notas técnicas confirman que no está implementado. Se registra como brecha.
- La especificación presenta UAT con datos ficticios; la nota de ambientes del 21/05/2026 afirma que solo producción está activa. Se prioriza la fuente más reciente.
- La regla promete ausencia de superposición, pero la implementación documentada no es transaccional y soporte registró duplicados. La garantía no se considera satisfecha.
- El resumen automático afirma que los dos duplicados fueron resueltos por huso horario; la transcripción confirma solo uno. El primero permanece sin causa verificada.
- La especificación y las notas técnicas describen el dashboard protegido por middleware; tras logout se observaron las tres rutas de dashboard todavía renderizadas. No se resuelve si es exposición de datos, caché/UI residual o protección incompleta.
- La especificación dice que la duración acepta cualquier entero positivo; la UI observada ofrece únicamente 15, 30, 45, 60, 90 y 120 minutos. Negocio debe confirmar cuál es la regla válida.
- El PRD reconstruido incluye carga manual de clientes; la UI muestra “Nuevo Cliente”, pero el botón no produjo un formulario ni cambio visible. La funcionalidad queda parcial o no verificada, no confirmada como implementada.

## Preguntas abiertas

- ¿Qué release objetivo se quiere definir: estabilización de lo existente o ampliación funcional?
- ¿Qué ocurre con turnos existentes al bloquear, cuál es la ventana de cancelación y hasta cuándo puede reservarse?
- ¿Cómo se modelan quien reserva para otro y varias agendas por organización?
- ¿Qué estado tendrá un no-show y qué recordatorio se enviará, cuándo y por qué canal?
- ¿Cuáles son los NFRs acordados de rendimiento, disponibilidad, concurrencia, accesibilidad y compatibilidad?
- ¿Qué incluye el Plan Pro y cómo se cobra?
- ¿Las rutas de dashboard deben redirigir inmediatamente al login y limpiar todo contenido al cerrar sesión?
- ¿“Nuevo Cliente” está pendiente, roto o restringido por una condición no visible?
- ¿La duración válida es cualquier entero o solo el conjunto ofrecido por la UI?

## Próximo paso

Continuar con `.prompts/2-Arquitectura/architecture-design.md`.
