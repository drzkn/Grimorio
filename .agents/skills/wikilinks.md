# Wikilinks (Obsidian)

Referencia compartida. Cargar con una línea al tocar caps fuente, notas, fichas, merge o informes. Solo Obsidian resuelve `[[ ]]`.

## Vault

Path: `AGENTS.md`. Cada relato = `<relato>/`. Wikilinks resuelven desde esa raíz.

## Sintaxis

- `[[ahumi|Ahumi]]`, `[[la_vigilante|La Vigilante]]` si ese nombre de fichero es único en el vault
- Si el mismo nombre existe en otro relato: `[[<relato>/contexto_global/personajes/ahumi|Ahumi]]`
- Target de ruta = camino desde la raíz del vault, **sin** `.md`
- Etiqueta = grafía que ve el lector

## Colisión de nombres

`1.md` existe en `<relato>/capítulos/` y en `<relato>/contexto_global/capitulos/`, y puede repetirse en otro relato. Siempre ruta desde la raíz del vault:

- `[[<relato>/capítulos/1|Capítulo 1]]`
- `[[<relato>/contexto_global/capitulos/1|Nota cap 1]]`

**Nunca `[[1]]`.**

## Quién lleva enlaces

| Sitio | Qué |
|-------|-----|
| Cap fuente (`capítulos/N.md`) | Primera mención de personaje con ficha + pie `## Relacionado` |
| Nota de cap | Plantilla de `contexto-capitulo` |
| Fichas de personaje | `Aparece en`, relaciones |
| Merge (`resumen`, historia, tono) | Primera mención + pie de resumen |
| Cabecera de análisis / lectura / redline | línea `**Fuente:**` |

Dueño del relink del cap fuente = skill `contexto-capitulo`.

## Pie de cap fuente (plantilla canónica)

Empieza en el `---` final seguido de `## Relacionado`:

```markdown
---
## Relacionado
- Nota: [[<relato>/contexto_global/capitulos/N|Nota cap N]]
- Anterior: [[<relato>/capítulos/N|Capítulo N]] · Siguiente: [[<relato>/capítulos/N|Capítulo N]]
- Personajes: [[ahumi|Ahumi]], …
```

Omitir Anterior/Siguiente si no aplica. Solo personajes con ficha en `contexto_global/personajes/`.

## El pie no es prosa

Ninguna skill lo analiza, puntúa, cuenta en palabras, cita, ilustra ni lo trata como cierre de capítulo. Cortar el capítulo en el `---` que abre `## Relacionado` antes de leer/analizar/ilustrar/redlinear.

## Citas siempre limpias

Al citar prosa con `>`, quitar el markup:

- `[[ahumi|Ahumi]]` → citar `Ahumi`
- Un ancla `>` de un análisis casa contra el texto **sin** wikilinks
- Un `>` con `[[ ]]` dentro = error de skill

## Primera mención

Un enlace por personaje y capítulo. Resto de menciones, texto plano. No inventar nombres que la prosa no dice (van en el pie si hay ficha, no inline).

## Notion

- Notion **no** lleva wikilinks propios.
- Al subir informes (`guarda-analisis`): copiar `[[ ]]` **literales**. No convertir, no borrar, no crear menciones Notion.
- Nunca escribir `[[ ]]` en las páginas de `Capítulos` ni en la raíz del relato.
- Corrección ortográfica en Notion: `old_str` = texto del fetch (sin wikilinks).

## Cabecera de informes

```markdown
**Fuente:** [[<relato>/capítulos/N|Capítulo N]] · [[<relato>/contexto_global/capitulos/N|Nota cap N]]
```

- `chapter-reader` / análisis / redline: un cap.
- `fantasy-reader`: lista de caps leídos con el mismo formato.

## Riesgo conocido

Volcado de Notion (`copia-capitulos`) pisa el cap fuente y borra enlaces + pie. Relink = `contexto-capitulo`.
