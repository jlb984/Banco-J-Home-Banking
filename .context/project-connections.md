# Conexiones oficiales del proyecto

Este archivo define los destinos canónicos de esta ejecución. Toda guía, prompt y
entregable operativo debe resolver las conexiones desde aquí o desde `AGENTS.md`.

| Servicio | Valor oficial |
| :--- | :--- |
| Jira | `https://jlb984.atlassian.net/` |
| Project Key de Jira | `BJHB` |
| GitHub | `https://github.com/jlb984/Banco-J-Home-Banking` |

## Regla de uso

* `BJHB` es el único proyecto Jira autorizado para nuevas lecturas, escrituras y
  sincronizaciones de este repositorio.
* El repositorio GitHub oficial es `jlb984/Banco-J-Home-Banking`; no se debe publicar
  esta ejecución en repositorios anteriores del curso.
* Las claves `CAQ-*` eran identificadores de una ejecución que se mezcló con este
  proyecto. El 03/09/2026 se compararon, deduplicaron y migraron a tickets reales de
  `BJHB`; el mapeo auditable está en `.context/PBI/migracion-caq-a-bjhb.md`.
* Las referencias operativas locales ya usan las claves reales de `BJHB`. Las claves
  anteriores solo deben aparecer como trazabilidad histórica de la migración.
* Ningún flujo debe leer o modificar `CAQ` como consecuencia de trabajar en este
  repositorio.

## Precedencia

Si otro documento editable contradice estos valores, prevalece este archivo. Los
archivos de `.context/Confluence-corporativo/` son un registro histórico inmutable y
pueden conservar nombres o referencias anteriores sin que eso cambie los destinos
oficiales.
