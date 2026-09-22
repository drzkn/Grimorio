---
name: contexto-capitulo
description: >-
  Crea o actualiza la nota de contexto de un capítulo en relatos/<relato>/contexto_global/capitulos/<N>.md.
  Es un snapshot wiki (qué pasó EN ese cap), no una skill de Cursor: se carga por ruta, no por índice.
  Úsalo cuando el usuario diga "guarda el contexto del capítulo", "crea skill del capítulo",
  "contexto-capitulo", "captura el capítulo", o cuando la IA termine de leer un capítulo entero
  (análisis, ilustración, build-context, copia, o lectura explícita).
---

# Contexto Capítulo

Tras leer un capítulo completo, **persistir lo extraído** en la wiki del relato. No re-leer el `.md` fuente en sesiones futuras si la nota está al día.

Respuesta al usuario en **español**.

## Dónde vive cada nota

```
relatos/<relato>/contexto_global/capitulos/<N>.md
```

Ejemplo: `relatos/el_tejedor_de_mareas/contexto_global/capitulos/1.md`

- `<relato>` = mismo nombre de carpeta que en `relatos/`
- `<N>` = número del capítulo, sin padding (`1`, `2`, `4`)
- Crear `contexto_global/capitulos/` si no existe
- Markdown plano. **No** `SKILL.md`, **no** YAML, **no** `.cursor/skills/`
- Cursor **no** las indexa. Cargar con Glob/Read
- Van a git con el resto de `contexto_global/`

Capas (no mezclar):

| Path | Pregunta |
|------|----------|
| `capítulos/<N>.md` | texto fuente |
| `contexto_global/capitulos/<N>.md` | ¿qué pasó *en* este cap? |
| `resumen.md` / `contexto_historia.md` / `personajes/` | ¿cómo está el mundo *después*? |

## Cuándo crear / actualizar

**Crear** si no existe `relatos/<relato>/contexto_global/capitulos/<N>.md`.

**Actualizar** (sobreescribir) si:
- El usuario lo pide explícitamente
- El `.md` fuente es más reciente que la nota (comparar mtime)
- El análisis o la lectura actual contradice lo guardado

**No tocar** si la nota existe, el capítulo no ha cambiado, y el usuario no pidió recaptura.

## Cuándo cargar (antes de re-leer el capítulo)

Al trabajar en un relato (edición, análisis, ilustración, contexto global, continuidad):

1. Glob `relatos/<relato>/contexto_global/capitulos/*.md`
2. Leer la nota del capítulo objetivo **y** las anteriores si hace falta continuidad
3. Leer también el merge (`resumen.md`, `contexto_historia.md`, `tono_narrador.md`, `personajes/`)
4. Solo leer el `.md` fuente si no hay nota, está desfasada, o el usuario pide el texto literal (citas, corrección, ilustración de una escena concreta)

## Flujo — capturar

1. **Identificar relato y capítulo.** Si no está claro, preguntar.
2. **Leer el capítulo** en `relatos/<relato>/capítulos/` (`N.md`, `capitulo_N.md`, `cap_N.md`).
3. **Leer `contexto.md`** si existe — reglas de mundo del autor. No contradecirlas en la nota.
4. **Extraer** solo lo que otra sesión necesitaría para no re-leer el capítulo. Sin copiar el texto entero.
5. **Escribir** `contexto_global/capitulos/<N>.md` con la plantilla de abajo.
6. **Informar**: relato, cap, ruta, si fue alta o update. 2-4 frases de qué se guardó. No volcar la nota completa al chat.

## Plantilla

```markdown
# <Título> — Capítulo <N>

**Fuente:** relatos/<relato>/capítulos/<N>.md
**Capturado:** <YYYY-MM-DD>

## Qué pasa
[3-6 frases. Hechos, no estilo. Sin spoilers de capítulos posteriores.]

## Personajes (estado en este cap)
- **<Nombre>:** [rol en la escena, cambio, dato nuevo. Grafía exacta del autor]

## Mundo / magia
- [Hechos nuevos o reglas aplicadas en ESTE capítulo]

## Tono
- [Voz, atmósfera, imágenes recurrentes de ESTE capítulo]

## Hilos
- Abiertos: [lo que este cap deja sin resolver]
- Cerrados: [lo que este cap cierra, si hay]

## Continuidad
- Depende de: [caps anteriores relevantes, o "ninguno"]
- Prepara: [qué deja listo para el siguiente]

## Imágenes / citas clave
> "[una o dos citas cortas, solo si anclan tono o un hecho crítico]"
```

### Reglas de la nota

- Concisa. Objetivo: **<120 líneas**. Si un apartado no aplica, omitirlo
- Nombres propios: grafía del autor / `contexto.md`
- Solo información que el lector ya conoce **en este capítulo**
- No copiar párrafos enteros del capítulo
- No duplicar el merge: aquí va el recorte de *este* cap, no el estado fusionado de la obra
- Sin frontmatter YAML

## Relación con otras skills

| Skill | Qué hacer |
|-------|-----------|
| `chapter-editor` | Tras analizar un cap, capturar/actualizar su nota |
| `build-context` | El merge tira **de** estas notas. Si falta nota o está desfasada, capturar primero; luego fusionar desde la nota. No re-leer el `.md` fuente para el merge si la nota está al día |
| `riso-illustration` | Cargar la nota del cap antes de leer el `.md` si está al día; si hay que citar escena visual, leer el `.md` |
| `copia-capitulos` | Tras copiar caps nuevos de Notion, capturar cada uno |

No bloquear el flujo principal: si el usuario pidió análisis/ilustración, entregar eso primero y capturar la nota al final del mismo turno.

## Captura en lote

Si el usuario pide contexto de varios caps o de un relato entero:

1. Listar caps en `relatos/<relato>/capítulos/`
2. Saltar los que ya tienen nota al día
3. Leer y escribir el resto, uno por uno
4. Informar: creadas / actualizadas / ya al día
