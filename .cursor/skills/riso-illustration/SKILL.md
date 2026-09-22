---
name: riso-illustration
description: Genera una ilustración con estética de risografía a partir de un capítulo y el contexto del relato. Usa GenerateImage de Cursor, guarda el PNG en relatos/<relato>/ilustraciones/. Úsalo cuando el usuario diga "ilustra el capítulo", "genera ilustración riso", "riso-illustration", "crea imagen risografía" o pida una ilustración para un capítulo de un relato.
---

# Riso Illustration

Genera la imagen. El prompt es interno (argumento de `GenerateImage`), no el entregable. Respuesta al usuario en **español**.

Generador: `GenerateImage` (namespace `cursor`). No usar MCP de imágenes.

## Flujo

1. **Detectar capítulo** — si el usuario no especifica ruta, preguntar qué capítulo ilustrar
2. **Leer capítulo** — leer el `.md` del capítulo
3. **Leer contexto** — `contexto.md` en la carpeta padre del capítulo (un nivel arriba de `capítulos/`). Si existe `contexto_global/`, leer merge (personajes, tono) y `capitulos/<N>.md` si está al día. El `.md` fuente sigue haciendo falta para citar la escena visual
4. **Extraer escena** — una sola escena, la más potente (ver "Selección de escena")
5. **Construir prompt** — ensamblar en inglés con la plantilla de abajo. No mostrarlo al usuario
6. **Generar imagen** — `GenerateImage` (namespace `cursor`):
   - Primero `GetDynamicTools` con `namespace: "cursor"`, `toolName: "GenerateImage"`
   - Leer schema. Luego `CallDynamicTool` con:
     - `description`: el prompt riso ensamblado
     - `aspect_ratio`: `"16:9"`
     - `filename`: `cap-N-riso.png` (N = número del capítulo)
   - El tool guarda un PNG y el cliente lo muestra
7. **Guardar en el relato** — copiar el PNG a `relatos/<relato>/ilustraciones/<N>.png`. Crear la carpeta si no existe. Si `<N>.png` ya existe, guardar como `<N>-2.png` (incrementar)
8. **Informar** — escena elegida (1-2 frases), paleta (COLOR_1 / COLOR_2), ruta del fichero. No volcar el prompt. No incrustar la imagen en markdown (el cliente la muestra solo)

Si hace falta **editar** una ilustración existente (el usuario pide cambios sobre un PNG ya generado): mismo tool `GenerateImage`. `reference_image_paths` = array con el path local del PNG, `description` = instrucciones de edición, `aspect_ratio` = `"16:9"`. Luego copiar el resultado al mismo esquema de `ilustraciones/`.

Si `GenerateImage` falla: mostrar el prompt en un bloque de código y decir qué falló.

## Selección de escena

Del capítulo, extraer **una sola escena** que cumpla al menos dos:
- Momento de alta carga emocional (nacimiento, pérdida, transformación, confrontación)
- Presencia de elementos visuales fuertes (agua, luz, criaturas, entornos inhóspitos)
- Punto de giro narrativo

Si hay varias candidatas, elegir la más cercana al clímax del capítulo. No componer escenas de acción rápida; preferir momentos de quietud dramática o contemplación.

## Plantilla de prompt

Ensamblar en inglés. Sustituir `[...]`. Va a `description` de `GenerateImage`, no al chat.

```
Risograph print illustration. [ESCENA_EN_UNA_FRASE].

Style: hand-crafted risograph poster. Ink overprint on off-white textured paper. [COLOR_1] and [COLOR_2] ink layers, slight misregistration creating halation. Coarse halftone dots on shadows. Grain and paper texture visible throughout. Flat areas of color with imperfect edges. No gradients — only solid tones and dot patterns.

Composition: [COMPOSICIÓN]. Negative space used intentionally. Lines are confident and slightly rough, like hand-cut stencils.

Mood: [ESTADO_EMOCIONAL]. The atmosphere should feel [ATMÓSFERA].

Characters: [DESCRIPCIÓN_PERSONAJES_SI_LOS_HAY]. Do not add faces unless the scene clearly requires them. Silhouettes preferred.

Setting: [ENTORNO]. Water, depth, coral, bioluminescence as appropriate.

Do not include text, logos, or letters. No photorealism. No 3D rendering.
```

No pedir ratio en el texto del prompt: ya va en `aspect_ratio` (`16:9`).

### Paleta por tipo de escena

| Tipo de escena | COLOR_1 | COLOR_2 | Acento opcional |
|---|---|---|---|
| Nacimiento / creación | Fluorescent pink | Teal | —  |
| Profundidad oceánica | Navy blue | Mint green | —  |
| Confrontación / ira | Burnt orange | Deep purple | —  |
| Muerte / funeral | Slate blue | Warm grey | —  |
| Transformación / magia | Fluorescent yellow | Dark teal | —  |
| Terror cósmico | Black | Acid yellow | —  |

Si la escena mezcla tipos, tomar los colores del tipo dominante.

### Descripción de personajes clave (referencia)

- **Ahumi**: figura estilizada, espalda ancha, piel bronceada oscura brillante, cabellos en cientos de trenzas finas agrupadas en coleta, colmillos prominentes en mandíbula inferior. En ilustración: silueta semitransparente o luminosa si está bajo el agua.
- **Khamate**: similar a Ahumi pero nariz larga con dientes de sierra a los lados, boca llena de colmillos, piel azulada. En ilustración: forma oscura con detalles dentados.
- **Raukami**: humanoides marinos, atléticos, armados con taiahas y me´res de jade.
- **Titán/Coloso**: entidad masiva, base para una civilización; no mostrar completo, solo fragmento de escala imposible.
- **La Vigilante**: no mostrar forma, solo presencia: corrientes, luz, geometría amenazante.

## Notas

- Si el capítulo no tiene ruta clara a `contexto.md`, usar solo el capítulo e indicarlo
- Preferir siluetas y composiciones simples sobre escenas detalladas — el estilo riso funciona mejor con formas claras
- Prompt en inglés (el modelo de imagen responde mejor)
- Entregable = PNG en `ilustraciones/` + imagen en el chat. Prompt solo si la generación falla
- No hace falta API key: `GenerateImage` va con Cursor
