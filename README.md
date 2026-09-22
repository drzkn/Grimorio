# Grimorio
Conjunto de skills para manejar el lore de distintos relatos.

Las skills viven en `.cursor/skills/`. Invocar por nombre o por la frase de cada descripción.

## Notion → local
- **copia-pagina** — Busca una página de Notion por nombre y la vuelca a `contenido.md` en el proyecto.
- **copia-capitulos** — Exporta la BD hija `Capítulos` a `capítulos/<Orden>.md` (un fichero por entrada).

## Contexto / lore
- **contexto-capitulo** — Snapshot wiki de un cap: `contexto_global/capitulos/<N>.md` (qué pasó *en* ese cap).
- **build-context** — Actualiza el merge de `contexto_global/` (resumen, historia, tono, personajes) a partir de esas notas. Incremental.

## Lectura (no edición)
- **chapter-reader** — Lee un capítulo como lector. Modos: beta / aficionado. Inmersión, ganas de seguir, si la gente importa.
- **fantasy-reader** — Igual, pero el relato entero.

## Edición
- **chapter-editor** — Análisis editorial de un cap (estructura, lore, prosa, nota /10). Guarda `analisis_capN.md`, corrige ortografía, captura contexto, dispara redline y espejo Notion.
- **capitulo-revisado** — Redline hacia ≥8/10 a partir de los ítems `🎯8`. Escribe `revision_capN.md`. No toca el cap canónico.
- **guarda-analisis** — Espeja informes locales en la BD `Revisiones` de Notion (un padre por cap, un toggle por informe). No genera el análisis.

## Ilustración
- **riso-illustration** — Ilustración riso de una escena del cap. PNG en `relatos/<relato>/ilustraciones/`.
