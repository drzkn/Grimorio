---
name: copia-pagina
description: Busca una página de Notion por nombre y vuelca su contenido en un archivo .md con el mismo nombre en el proyecto. Sobreescribe el archivo si ya existe. Usar cuando el usuario diga "copia página", "volcar página de Notion", "copia-pagina" o pida exportar una página de Notion a markdown.
---

# Copia Página

Buscar página Notion por nombre → volcar contenido como `.md` en el proyecto.

## Flujo

1. **Preguntar nombre** si el usuario no lo proporcionó
2. **Buscar en Notion** con `notion-search` (query = nombre de página, `content_search_mode: workspace_search`, `page_size: 5`)
3. **Seleccionar resultado** — tomar el primer resultado cuyo título coincida exactamente o sea el más cercano. Si hay ambigüedad, mostrar opciones y pedir confirmación
4. **Fetch completo** con `notion-fetch` usando el `id` del resultado
5. **Determinar tipo de página** → ver sección "Detectar tipo" más abajo
6. **Calcular ruta destino** — `<raíz>/<tipo>/<nombre>/contenido.md`
7. **Crear carpeta** si no existe (usando shell `mkdir -p <tipo>/<nombre>`)
8. **Comprobar si existe** el archivo en esa ruta
   - Si existe → advertir al usuario e indicar que se sobreescribirá, luego proceder
   - Si no existe → crear directamente
9. **Escribir el archivo** con el contenido completo obtenido del fetch
10. **Confirmar** indicando ruta final del archivo creado/sobreescrito

## Nombre de archivo

Convertir título de la página a nombre de archivo:
- Minúsculas
- Espacios → `_`
- Eliminar caracteres especiales excepto `-` y `_`
- Extensión `.md`

Ejemplo: `"El tejedor de mareas"` → `el_tejedor_de_mareas.md`

## Detectar tipo

Determinar la carpeta destino en este orden de prioridad:

1. **Base de datos padre** — si la página pertenece a una base de datos Notion, usar el nombre de la BD en snake_case como carpeta (ej: base de datos "Relatos" → carpeta `relatos/`)
2. **Propiedad "Tipo"** — si la página tiene una property llamada `Tipo`, `Type`, `Categoría` o `Category`, usar su valor en snake_case
3. **Página padre** — si la página está dentro de otra página de Notion, usar el título de la página padre en snake_case
4. **Fallback** — si nada de lo anterior aplica, guardar en la raíz del workspace sin subcarpeta

Raíz del workspace: `/Users/diegor/Proyectos/IRU/`

Ejemplo completo:
- Página "El tejedor de mareas" en BD "Relatos" → `relatos/el_tejedor_de_mareas/contenido.md`
- Página "Kael" con Tipo = "Personaje" → `personaje/kael/contenido.md`
- Página "Notas sueltas" sin BD ni tipo → `notas_sueltas/contenido.md`

## Notas

- Usar siempre `content_search_mode: workspace_search` para búsquedas más rápidas
- El contenido del fetch ya viene en Markdown — volcar tal cual, sin transformar
- Si la búsqueda no devuelve resultados, informar al usuario y sugerir variantes del nombre
- El tipo/carpeta se deriva de metadatos Notion, no se infiere del contenido del texto
