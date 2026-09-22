---
name: copia-capitulos
description: Exporta los capítulos de una página Notion a archivos .md individuales. Si la página tiene una base de datos hija llamada "capítulos", crea una carpeta capítulos/ y dentro un archivo por cada entrada, usando el valor de la propiedad Orden como nombre de archivo. Usar cuando el usuario diga "copia capítulos", "exportar capítulos", "volcar capítulos de Notion", "copia-capitulos" o pida exportar los capítulos de una obra de Notion.
---

# Copia Capítulos

Buscar página Notion por nombre → detectar BD hija "capítulos" → volcar cada capítulo como `.md` individual.

## Flujo

1. **Preguntar nombre** si el usuario no lo proporcionó
2. **Buscar en Notion** con `notion-search` (query = nombre de página, `content_search_mode: workspace_search`, `page_size: 5`)
3. **Seleccionar resultado** — tomar el primer resultado cuyo título coincida exactamente o sea el más cercano. Si hay ambigüedad, mostrar opciones y pedir confirmación
4. **Fetch completo** con `notion-fetch` usando el `id` del resultado
5. **Determinar tipo y nombre** → ver sección "Detectar tipo" más abajo
6. **Localizar BD hija "capítulos"** — buscar en los bloques del fetch un bloque de tipo `child_database` cuyo título sea `Capítulos` o `capítulos` (case-insensitive)
   - Si no existe → informar al usuario y detener
7. **Obtener páginas de la BD** con `notion-query-database` usando el ID de esa BD hija
8. **Para cada página** de la BD:
   a. Fetch individual con `notion-fetch` usando el `id` de cada página
   b. Leer propiedad `Orden` (case-insensitive)
   c. Calcular nombre de archivo desde `Orden` → ver sección "Nombre de archivo"
   d. Ruta destino: `<raíz>/<tipo>/<nombre>/capítulos/<nombre_archivo>.md`
9. **Crear carpeta** `<tipo>/<nombre>/capítulos/` si no existe (`mkdir -p`)
10. **Para cada archivo**: comprobar si existe → advertir sobreescritura si aplica, luego escribir
11. **Relink / aviso wikilinks** — ver nota abajo
12. **Confirmar** con lista de todos los archivos creados/sobreescritos y sus rutas

## Nombre de archivo

Usar el valor de la propiedad `Orden` de cada página:

- Número (ej: `3`) → `3.md`
- Texto (ej: `"Prólogo"`) → snake_case sin tildes ni especiales → `prologo.md`
- Vacío o ausente → usar el título de la página en snake_case como fallback

## Detectar tipo

Determinar la carpeta destino de la página padre en este orden de prioridad:

1. **Base de datos padre** — nombre de la BD en snake_case (ej: "Relatos" → `relatos/`)
2. **Propiedad "Tipo"** — valor de property `Tipo`, `Type`, `Categoría` o `Category` en snake_case
3. **Página padre** — título de la página padre en snake_case
4. **Fallback** — raíz del workspace sin subcarpeta

Raíz del workspace: `/Users/diegor/Proyectos/IRU/`

Ejemplo completo:
- Página "El tejedor de mareas" en BD "Relatos", con BD hija "Capítulos" (Orden: 1, 2, 3) → `relatos/el_tejedor_de_mareas/capítulos/1.md`, `…/2.md`, `…/3.md`
- Misma página con capítulo de Orden "Prólogo" → `relatos/el_tejedor_de_mareas/capítulos/prologo.md`

## Notas

- Usar siempre `content_search_mode: workspace_search` para búsquedas más rápidas
- El contenido del fetch ya viene en Markdown — volcar tal cual, sin transformar
- Si la página no tiene BD hija "capítulos", informar al usuario (sugerir usar `copia-pagina` en su lugar)
- El tipo/carpeta se deriva de metadatos Notion, no del contenido del texto
- **Wikilinks:** ver [wikilinks.md](../wikilinks.md). Notion no lleva `[[wikilinks]]`. Un volcado pisa `capítulos/N.md` y borra pie `## Relacionado` + primeras menciones enlazadas. **No escribir Notion** para reponerlos.
  1. Antes de sobreescribir: si el `.md` local ya tenía `## Relacionado`, anotarlo.
  2. Tras volcar: listar los caps que **tenían** pie y lo han perdido.
  3. Encadenar skill `contexto-capitulo` para relink de esos caps (y de los nuevos sin pie).
  4. Si el usuario **no** quiere relink: avisar de que el grafo Obsidian queda roto hasta que corra `contexto-capitulo`.
