---
name: iniciar-relato
description: >-
  Fija el relato activo del workspace en .cursor/relato-activo.md (slug, nombre,
  ruta, query Notion). El resto de skills leen ese fichero; no nombran obras.
  Úsalo al empezar, al cambiar de relato, si falta relato-activo.md, o cuando
  el usuario diga "iniciar relato", "cambia de relato", "relato activo" o
  "iniciar-relato".
---

# Iniciar Relato

Punto de entrada del pack. **Una obra activa por workspace.** Skills de análisis, contexto, copia, lectura e ilustración leen `.cursor/relato-activo.md` y no preguntan el relato si ya hay uno.

Respuesta al usuario en **español**.

## Fichero canónico

```
.cursor/relato-activo.md
```

Plantilla (YAML + una línea de ayuda):

```markdown
---
slug: <snake_case>
nombre: <título para chat y Notion>
ruta: relatos/<slug>
notion_query: <título de la página Notion, suele coincidir con nombre>
---

Relato activo. Cambiar con la skill iniciar-relato.
```

- `slug`: nombre de carpeta. minúsculas, `_`, sin tildes.
- `nombre`: título humano.
- `ruta`: relativa a la raíz del repo. Default `relatos/<slug>`.
- `notion_query`: string para `notion-search`. Default = `nombre`.

Git-ignored. No commitear. No hardcodear un relato dentro de otras skills.

## Cuándo correr

| Situación | Acción |
|-----------|--------|
| Falta `.cursor/relato-activo.md` | Crear (flujo abajo) |
| Usuario nombra un relato distinto al activo | Sobreescribir el fichero |
| Usuario dice cambiar / iniciar / relato activo | Flujo abajo |
| Fichero existe y el mensaje no nombra otra obra | **No preguntar.** Devolver los campos y seguir |

Otras skills: primer paso = esta tabla. Si hay que crear o cambiar, hacerlo **antes** de localizar capítulos.

## Flujo

1. **Leer** `.cursor/relato-activo.md` si existe.
2. **Resolver el relato:**
   - El usuario dio un nombre → ese.
   - Si no, y hay fichero válido → usar esos campos. Usuario invocó solo esta skill → informar en una línea y parar. Otra skill pidió el relato → seguir con esa skill.
   - Si no: glob `relatos/*/` (carpetas). Una sola → proponerla. Varias → listar slugs y preguntar. Ninguna → preguntar título.
3. **Normalizar**
   - `slug`: minúsculas, espacios → `_`, quitar tildes y caracteres raros.
   - `nombre`: título tal cual el usuario (o el de la carpeta humanizado).
   - `ruta`: `relatos/<slug>` salvo que el usuario dé otra.
   - `notion_query`: `nombre`, salvo override.
4. **Carpeta** `ruta/`:
   - Si no existe: `mkdir -p <ruta>/capítulos`. El resto (`contexto_global/`, `lectura/`, `ilustraciones/`) lo crean otras skills cuando haga falta.
   - Si existe: no tocar contenido.
5. **Escribir** `.cursor/relato-activo.md` con la plantilla. Sobreescribir.
6. **Informar:** nombre, slug, ruta, si la carpeta era nueva o ya estaba. 2–4 líneas. No volcar el YAML al chat salvo que el usuario lo pida.

## Contrato para otras skills

Campos a usar (no re-derivar a ojo si el fichero los trae):

| Campo | Uso |
|-------|-----|
| `ruta` | Carpeta local del relato (`capítulos/`, `contexto_global/`, `lectura/`, `ilustraciones/`) |
| `nombre` | Informes, cabeceras, chat |
| `slug` | Nombres de fichero si hace falta |
| `notion_query` | `notion-search` |

Raíz de paths = **raíz del repo** (cwd del workspace). Nunca un path absoluto de otra máquina.

Si el usuario nombra un capítulo y no un relato, y hay activo: usar el activo.

## No hacer

- Meter título, personajes o lore de una obra concreta en esta skill ni en las demás.
- Preguntar el relato en cada skill si el fichero ya existe.
- Crear `contexto_global/` vacío de dummy. Eso lo hace `build-context` / `contexto-capitulo`.
