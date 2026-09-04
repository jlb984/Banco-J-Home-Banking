# Migración y deduplicación del backlog hacia BJHB

**Fecha:** 03/09/2026

**Jira destino:** `https://jlb984.atlassian.net/`

**Project Key destino:** `BJHB`

## Resultado

Se detectó que el repositorio contenía trabajo sincronizado anteriormente con el proyecto
`CAQ`. Se comparó ese material con el backlog real de `BJHB` y se aplicó una migración con
deduplicación:

* `BJHB-1`, `BJHB-2` y `BJHB-3` ya existían y eran equivalentes o versiones anteriores del
  material heredado. Se conservaron y se enriquecieron con el contenido refinado.
* Se crearon tres Epics y 21 Stories que no tenían equivalente en `BJHB`.
* Las cinco Epics y las 22 Stories quedaron vinculadas con la jerarquía correcta.
* Los archivos locales, planes de prueba e inspecciones ahora usan las claves reales de
  `BJHB`.
* Cada Story recibió en Jira su reporte de inspección Shift-Left y la decisión específica
  del PO para el próximo release.
* No se realizó una sustitución aritmética de prefijos: las claves fueron registradas desde
  las respuestas reales de Jira.

## Mapeo de Epics

| Referencia anterior | Clave BJHB | Tratamiento |
| :--- | :--- | :--- |
| `CAQ-2` | `BJHB-1` | Epic existente, actualizada |
| `CAQ-7` | `BJHB-3` | Epic existente, actualizada |
| `CAQ-8` | `BJHB-4` | Epic creada |
| `CAQ-9` | `BJHB-5` | Epic creada |
| `CAQ-10` | `BJHB-6` | Epic creada |

## Mapeo de Stories

| Referencia anterior | Clave BJHB | Tratamiento |
| :--- | :--- | :--- |
| `CAQ-3` | `BJHB-2` | Story existente; se integró la versión refinada |
| `CAQ-4` | `BJHB-11` | Story creada |
| `CAQ-5` | `BJHB-12` | Story creada |
| `CAQ-6` | `BJHB-13` | Story creada |
| `CAQ-11` | `BJHB-15` | Story creada |
| `CAQ-12` | `BJHB-14` | Story creada |
| `CAQ-13` | `BJHB-16` | Story creada |
| `CAQ-14` | `BJHB-17` | Story creada |
| `CAQ-15` | `BJHB-18` | Story creada |
| `CAQ-16` | `BJHB-19` | Story creada |
| `CAQ-17` | `BJHB-20` | Story creada |
| `CAQ-18` | `BJHB-21` | Story creada |
| `CAQ-19` | `BJHB-22` | Story creada |
| `CAQ-20` | `BJHB-23` | Story creada |
| `CAQ-21` | `BJHB-24` | Story creada; conserva la evidencia de cancelación |
| `CAQ-22` | `BJHB-25` | Story creada |
| `CAQ-23` | `BJHB-27` | Story creada |
| `CAQ-24` | `BJHB-26` | Story creada |
| `CAQ-25` | `BJHB-7` | Story creada |
| `CAQ-26` | `BJHB-9` | Story creada |
| `CAQ-27` | `BJHB-8` | Story creada |
| `CAQ-28` | `BJHB-10` | Story creada |

## Regla posterior

Toda lectura o escritura futura debe dirigirse exclusivamente a `BJHB`. Las referencias
`CAQ-*` de este archivo son evidencia histórica de la migración y no tickets activos para
esta ejecución.
