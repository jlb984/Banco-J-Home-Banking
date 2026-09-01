---
name: documentar-historia
description: Documenta una historia de usuario que ya está construida en la aplicación pero no existe como ticket ni como especificación, explorándola en el navegador y dejando la evidencia de lo observado. Úsala cuando el software exista y la documentación no, cuando haya que reconstruir el backlog de un proyecto heredado, cuando una historia esté marcada "Sin verificar", o cuando pidan "documentá esta pantalla", "armá la historia de lo que ya está hecho", "esto no está en Jira" o "andá a ver cómo funciona".
---

# Documentar una historia que ya está construida

En un proyecto heredado el software llegó antes que el papel. La funcionalidad existe, la usan
personas reales, y no hay ni ticket ni criterio de aceptación que diga qué se esperaba de ella.
Esta skill escribe ese papel mirando la aplicación.

El riesgo no es equivocarse en la redacción. Es este:

> **Que la aplicación haga X no convierte a X en un criterio de aceptación.** Lo convierte en
> un hecho que hay que confirmar. Si contradice a un documento, es un hallazgo. Si ningún
> documento lo respalda, es una pregunta abierta.

**Un defecto documentado como requisito deja de ser un defecto para siempre**, porque nadie lo
vuelve a reportar: el papel dice que funciona así. Es la forma más común de arruinar la
documentación de un proyecto heredado, y es exactamente lo que esta skill podría causar si se
usa sin cuidado.

---

## Antes que nada: cuál es tu trabajo y cuál no

Hay otro flujo en este repositorio que también abre el navegador sobre una historia, y no es
este. La diferencia es qué existe antes y qué queda después:

| | Explora para… | Necesita que el `story.md`… | Deja |
| :--- | :--- | :--- | :--- |
| **Esta skill** | **especificar** lo que nadie escribió | **no** exista, o esté `Sin verificar` | el `story.md` |
| **Testing exploratorio** (Fase 6) | **encontrar defectos** contra lo escrito | **sí** exista y esté refinado | reporte de sesión y bugs |

Una escribe la vara; la otra mide contra ella. **En un proyecto heredado esta corre primero**,
porque sin ella las fases de testing no tienen contra qué contrastar.

Si la historia ya está escrita y refinada, esto no es trabajo para acá: decilo y parás.

---

## Paso 1 · Leé lo que ya está escrito

Antes de preguntar nada:

1. **`.context/PBI/epic-tree.md`** — el backlog. Mostrame las historias con su campo
   `Implementación`, para que elijamos sobre qué trabajar.
2. **`.context/infrastructure/environments.md`** — **de ahí sale la URL y el nombre real del
   entorno.** No me los pidas.
3. **`.context/infrastructure/test-data-strategy.md`** — de ahí salen los usuarios de prueba.
   **Nunca me pidas una contraseña por chat ni abras un archivo de entorno para leerla:** se
   referencia como variable.
4. **La documentación heredada del proyecto** — la misma carpeta que usaron las fases de
   análisis. **Sin esto no podés hacer tu trabajo**, solo describir pantallas: es lo único que
   te permite distinguir *lo que se acordó* de *lo que quedó así*.

Si falta el mapa de entornos, **detenete**: no salgas a adivinar una dirección. Decime qué
archivo falta y qué prompt lo genera.

Solo entonces preguntame lo que no está escrito en ningún lado: **qué funcionalidad vamos a
documentar**.

## Paso 2 · Comprobá que esto sea trabajo para acá

Mirá si ya existe un `story.md` para esa funcionalidad.

| Lo que encontrás | Qué hacés |
| :--- | :--- |
| No existe nada | Historia nueva. Seguí. |
| Existe con `Implementación: Sin verificar` | Seguí: vas a completar lo observado sobre lo que ya está escrito, **sin borrar lo que dice**. |
| Existe, refinada y verificada | **Parás.** Está documentada. Si lo que hace falta es probarla, es testing exploratorio. |

## Paso 3 · Comprobá vos mismo si tenés navegador

**Revisá tus herramientas disponibles; no me lo preguntes a mí.**

**Con un MCP de navegador (Playwright):** navegás vos y sacás las capturas.

**Sin él:** no te detengas y no me pidas que lo instale. Guiame paso a paso para que lo
recorra yo, y **registrá solamente lo que yo te reporte**. Anotá el modo en el entregable.

> **Sin navegador no inventás comportamiento.** Si no lo viste y yo no te lo conté, no se
> escribe. Un criterio de aceptación deducido de cómo suele funcionar una pantalla de login es
> exactamente el error que esta skill existe para evitar.

## Paso 4 · Explorá para especificar

**No vengas a romper el sistema.** Eso es testing exploratorio y es otro momento. Acá estás
levantando acta de qué hace la funcionalidad cuando se usa como se espera, y de qué defiende
cuando no.

Recorré, en este orden:

1. **El camino principal, completo, hasta el final.** Dónde empieza, qué pide, dónde termina y
   qué queda cambiado después.
2. **Qué datos pide y cuáles son obligatorios.** Qué pasa si dejás uno vacío.
3. **Qué valida y con qué mensaje.** Transcribí los textos **literales**: un mensaje de error
   es un requisito escrito por alguien, aunque ese alguien haya sido el desarrollador.
4. **Qué te impide hacer.** Lo que el sistema rechaza dice tanto como lo que acepta.
5. **A dónde te lleva después** y qué ve el otro rol, si hay más de uno.

Dos límites, y los dos importan:

- **Poné un tope de tiempo y respetalo.** Si a los 30-40 minutos seguís descubriendo, cerrá lo
  que tenés y anotá el resto como pendiente. Una historia documentada hoy vale más que tres a
  medio mirar.
- **Fijate qué entorno estás tocando.** Si el mapa de entornos dice que no hay uno separado,
  **estás en el mismo lugar que los usuarios reales**: lo que cargues queda, y los avisos que
  dispares salen de verdad. Decímelo antes de crear nada.

**La evidencia no es opcional.** Una captura por cada afirmación que vayas a escribir, en
`.context/PBI/epics/[EPIC]/stories/[STORY]/evidence/`, con el nombre
`[fecha]-[escenario-slug].png`. Una afirmación sin captura no se escribe como observada.

## Paso 5 · Clasificá cada dato antes de escribirlo

Este es el paso que hace que el entregable sirva. Para **cada** cosa que vayas a afirmar,
decidí de dónde salió:

| Origen | Cuándo | Cómo se registra |
| :--- | :--- | :--- |
| **Documento** | Un documento del proyecto lo dice | `archivo.md` · sección |
| **Observado** | Lo viste en la aplicación | `**Observado**` — entorno, fecha, ruta de la captura |
| **Hipótesis** | Lo dedujiste, no lo viste ni lo leíste | `**Hipótesis**` — y además una pregunta abierta |

Y después cruzá las dos primeras columnas, porque **ahí está el valor de todo esto**:

- **Coinciden** → criterio de aceptación sólido. Citá las dos fuentes.
- **Se contradicen** → **hallazgo**. Escribí las dos versiones y **no elijas**: no sabés si el
  sistema está mal o el documento quedó viejo. Va a *Contradicciones detectadas* y a
  *Preguntas abiertas*.
- **Observado sin documento** → se escribe como observado, **nunca como acordado**, y genera
  una pregunta abierta. Que funcione así no significa que deba funcionar así.
- **Documento sin observar** → puede que no esté construido. Eso decide el veredicto del
  Paso 6.

## Paso 6 · Escribí el `story.md`

En `.context/PBI/epics/[EPIC]/stories/STORY-[ID]-[nombre-kebab-case]/story.md`, con **el mismo
formato que usa el resto de la fase de especificaciones** — leelo de los prompts de esa fase en
lugar de inventarlo, para que las fases siguientes lo puedan consumir.

Tres cosas propias de esta skill:

**El veredicto**, en el encabezado:

| Valor | Cuándo |
| :--- | :--- |
| `Implementada` | La recorriste entera y hace lo que la historia describe |
| `Parcial` | Existe, pero le falta algo que los documentos declaran |
| `No encontrada` | La buscaste y no está. **No es lo mismo que no existir**: decí dónde buscaste |
| `Sin verificar` | No llegaste a mirarla. No la marques de otra forma para cerrar el archivo |

**La sección de contraste**, que es lo que ningún otro prompt produce:

```markdown
## Comportamiento observado
| Qué hace | Evidencia | Qué decía la documentación |
| :--- | :--- | :--- |
| [Comportamiento] | `evidence/[archivo].png` | [Cita, o **nada: ningún documento lo menciona**] |
```

**Y las tres secciones de cierre** que la fase nunca omite: `## Fuentes`,
`## Contradicciones detectadas` y `## Preguntas abiertas`. Si alguna queda vacía se escribe
*"Ninguna detectada"*, no se borra.

## Paso 7 · Reportá y encadená

Decime, en la confirmación y no solo dentro del archivo:

- **La ruta del archivo** y cuántas capturas dejaste.
- **El veredicto** y en qué te basaste.
- **Cuántas contradicciones** encontraste entre lo que viste y lo que estaba escrito.
- **Qué quedó sin mirar** y por qué.
- **Si esto todavía no está en la herramienta de gestión**, decilo acá: el archivo local no
  avisa solo.

Y sugerí el paso siguiente: refinar la historia para pasarla a criterios de aceptación
formales, que es el prompt de refinamiento de la fase de especificaciones.

---

## Nunca

- **Nunca escribas un comportamiento como criterio de aceptación sin haberlo contrastado**
  contra la documentación. Ese es el error que esta skill puede causar.
- **Nunca resuelvas vos una contradicción** entre lo que viste y lo que está escrito. Reportala.
- **Nunca inventes el "para qué".** El *"Como… quiero… para…"* necesita un motivo de negocio, y
  eso no se lee en una pantalla. Si ningún documento lo dice, escribilo como pregunta abierta
  en lugar de completarlo con algo plausible.
- **Nunca marques `Implementada` sin haber recorrido el camino entero.** Que exista el botón no
  significa que el flujo termine bien.
- **Nunca cargues datos de prueba masivos** sin avisar antes en qué entorno estás.
- **Nunca escribas una credencial** en el `story.md`, ni siquiera de un usuario de prueba.
