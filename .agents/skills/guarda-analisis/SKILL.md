---
name: guarda-analisis
description: >-
  Espeja análisis de lectura y edición en Notion: una fila de Revisiones por
  capítulo («Análisis — Cap N»), cada informe en un toggle heading. Úsalo al
  terminar chapter-editor, chapter-reader, fantasy-reader o
  promesa-progreso-recompensa, o cuando el usuario
  diga "sube el análisis", "guarda feedback en Notion", "guarda-analisis" o
  "sube todos los análisis".
---

# Guarda Análisis

Espejo local → Notion. **No genera** el análisis. Fuente = ficheros `.md` locales.

**Invariante:** un padre Notion **por capítulo** (o uno `Relato`), **fila de la BD hija `Revisiones`**, título con el cap. Cada informe = **un toggle heading 2** en ese padre. Capitulos queda intacto.

Respuesta al usuario en **español**.

## Padres

| Alcance | Título de la fila (`Name`) |
|---------|----------------------------|
| capítulo `{N}` | `Análisis — Cap {N}` |
| relato entero | `Análisis — Relato` |

`{N}` sin padding (`1`, no `01`). Raya em `—`, igual que las claves de toggle.

Esa fila vive **dentro** de `Revisiones` (`parent.data_source_id` = el `collection://` de esa BD). Completado cuando el fetch del padre muestra `parent-data-source` = Revisiones y el título coincide.

## Flujo

1. **Relato + tipo + cap** (o relato entero). Relato = skill `iniciar-relato` / `.cursor/relato-activo.md`. Si viene de otra skill, ya lo sabe. Si falta tipo o cap, preguntar.
2. **Leer el `.md` local** (tabla «Claves»). Si no existe → parar. Esta skill no escribe el informe.
3. **Buscar el relato** en Notion: `notion-search` (query = `notion_query` del relato activo, `page_size: 5`). Mismo criterio que `copia-capitulos`. Ambigüedad → pedir confirmación.
4. **`notion-fetch` del relato.** Localizar la BD hija `Revisiones` (título exacto case-insensitive; tag `<database …>Revisiones</database>` con `data-source-url="collection://…"`).
   - Si no hay → parar y avisar. No crear esa BD. No crear página suelta bajo el relato.
5. **`notion-fetch` de `Revisiones`** (URL del tag). Leer schema y opciones. Completado: lista de propiedades reales, sin inventar ninguna.
6. **Padre:** `notion-query-data-sources` sobre ese `collection://`. Buscar fila cuyo `Name` sea el título de «Padres» (exacto, case-insensitive).
   - Si hay → usarla.
   - Si no → `notion-create-pages` con `parent.data_source_id` = UUID del `collection://`, `icon`: `📝`, `content` vacío, propiedades según «Mapping Revisiones». Luego fetch.
   - Legado: fila o página hija titulada solo `Análisis`. No crear otra así. Si su cuerpo es solo de este cap (o Relato), `update_properties` al título canónico y usarla. Si mezcla caps, crear la fila canónica, mover a ella los toggles de este alcance, y dejar en la vieja una línea que apunte a la nueva. `notion-move-pages` si el legado cuelga del relato y no de Revisiones.
7. **Raíz del relato:** no añadir `<mention-page>` de análisis junto a Capitulos / Revisiones / Roadmap. Si hay una mención huérfana a un `Análisis` suelto, quitarla (`update_content`). Revisiones ya es el índice.
8. **`notion-fetch` del padre.**
9. **Armar el toggle** (sección «Título y cuerpo»).
10. **Upsert** en **ese** padre:
    - Existe heading cuya línea empieza por `## {clave}` → `update_content`: `old_str` = ese toggle entero (heading + hijos indentados hasta el siguiente `## ` de nivel 2 o EOF). `new_str` = toggle nuevo.
    - No existe → insertar en el hueco de **orden** (sección «Orden»). Si no se puede calcular, `insert_content` al final.
    - Dos headings con la misma clave → parar y avisar.
11. **Fetch otra vez.** Completado: heading presente, hijos con tab, resto de toggles de **este** padre intactos, título canónico, padre = fila de Revisiones.
12. Devolver URL del padre + título del toggle escrito.

**Bulk** («sube todos»): agrupar por padre (`Cap {N}` vs `Relato`). Por cada grupo, pasos 6–11.

## Mapping Revisiones

Fetch del schema **en cada run**. Rellenar solo propiedades que existan. No crear propiedades.

Baseline (schema típico de una BD Relatos):

| Propiedad | Tipo | Al crear | Al reusar |
|-----------|------|----------|-----------|
| `Name` | title | título canónico de «Padres» | si es legado `Análisis`, renombrar; si ya es canónico, no tocar |
| `Status` | status: `Not started` / `In progress` / `Done` | `Not started` | no cambiar |
| `Created` | created_time | no setear | no setear |

Cap, fecha y nota **no** son propiedades de esta BD: van en el título de la fila y en el toggle.

Si otro relato tiene más columnas (tipo, capítulo, fecha, nota): leer filas existentes (p. ej. `Capitulo 3`) y opciones reales. Valor de tipo = el que ya use análisis/revisión, o la opción más cercana; si ninguna encaja, dejar vacío y decirlo. Nunca inventar una opción.

## Claves y ficheros

Clave = texto del heading **sin fecha**. Match = `starts with` `## {clave}`.

`<ruta>` = campo `ruta` de `.cursor/relato-activo.md`.

| Tipo | Clave | Fichero | Padre |
|------|--------|---------|-------|
| edición cap | `Edición — Cap {N}` | `<ruta>/analisis_cap{N}.md` | `Análisis — Cap {N}` |
| lectura cap | `Lectura beta — Cap {N}` | `<ruta>/lectura/beta_cap{N}.md` | `Análisis — Cap {N}` |
| lectura cap | `Lectura aficionado — Cap {N}` | `<ruta>/lectura/aficionado_cap{N}.md` | `Análisis — Cap {N}` |
| lectura relato | `Lectura beta — Relato` | `<ruta>/lectura/beta.md` | `Análisis — Relato` |
| lectura relato | `Lectura aficionado — Relato` | `<ruta>/lectura/aficionado.md` | `Análisis — Relato` |
| PPR cap | `PPR — Cap {N}` | `<ruta>/analisis_ppr_cap{N}.md` | `Análisis — Cap {N}` |
| PPR relato | `PPR — Relato` | `<ruta>/analisis_ppr.md` | `Análisis — Relato` |

Fecha = día de la subida, `YYYY-MM-DD`.

Título completo:

```
## {clave} — {YYYY-MM-DD} {toggle="true"}
```

Ejemplo: `## Lectura beta — Cap 1 — 2026-09-16 {toggle="true"}`

Overwrite: misma clave, fecha nueva en el título. Un solo toggle por clave **en ese padre**.

## Orden en el padre

Página `Análisis — Cap {N}`:

1. `Edición — Cap {N}`
2. `Lectura beta — Cap {N}`
3. `Lectura aficionado — Cap {N}`
4. `PPR — Cap {N}`

Página `Análisis — Relato`:

1. `Lectura beta — Relato`
2. `Lectura aficionado — Relato`
3. `PPR — Relato`

Al insertar uno nuevo, colocarlo según esa lista (después del anterior existente, antes del siguiente). No reordenar el resto.

## Título y cuerpo

Toggle heading 2. **Hijos indentados con un tab.** Sin tab, Notion saca el bloque del toggle y rompe el invariante.

```
## Lectura beta — Cap 1 — 2026-09-16 {toggle="true"}
	**Modo:** beta
	**Nota:** 6 / 10
	---
	## De un tirón
	[sensación de apertura]
	## Momentos
	> "[cita del capítulo]"
	🔥 [sensación]
```

Conversión desde el `.md` local:

- Quitar el `#` del fichero (el título vive en el heading del toggle).
- Cada línea del resto: un tab al inicio.
- **No** envolver el informe en ` ```markdown `.
- Citas multilínea: `<br>` dentro del mismo `>`, no saltos crudos.
- `---` = divider. Vale.
- No inventar `<empty-block/>` salvo que el fetch ya lo tenga.
- Headings internos (`##`, `###`) se quedan, ya indentados: viven *dentro* del toggle.
- Espejo: no reescribir el análisis al subirlo.

## No hacer

- Página suelta por informe o por tipo (edición / beta / aficionado).
- Página hija del relato titulada solo `Análisis`.
- Mencionar análisis en la raíz del relato como hermano de Capitulos / Revisiones / Roadmap.
- Meter análisis en `Capitulos` (rompe `copia-capitulos`).
- Crear la BD `Revisiones` si falta, o una BD nueva si ya existe.
- `replace_content` de un padre que ya tiene toggles.
- Duplicar una clave en el mismo padre.
- Crear el informe si falta el `.md`.

## Hooks

Tras guardar el `.md` local, las skills de análisis **ejecutan esta skill** (un toggle en el padre de su alcance):

- `chapter-editor` → padre `Análisis — Cap {N}`, toggle `Edición — Cap {N}`
- `chapter-reader` → padre `Análisis — Cap {N}`, toggle `Lectura {modo} — Cap {N}`
- `fantasy-reader` → padre `Análisis — Relato`, toggle `Lectura {modo} — Relato`
- `promesa-progreso-recompensa` → padre `Análisis — Cap {N}` o `Análisis — Relato`, toggle `PPR — Cap {N}` o `PPR — Relato`
