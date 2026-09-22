---
name: capitulo-revisado
description: >-
  Reescribe un capítulo hacia ≥8/10 a partir de los ítems 🎯8 del análisis
  editorial, marca altas en rojo y bajas en gris tachado, y sube esa versión al
  toggle «Capítulo revisado — Cap N» de Análisis — Cap N. Úsalo al terminar
  chapter-editor, o cuando el usuario pida «capítulo revisado», «versión
  revisada», «redline», «versión 8/10» o «reescribe el capítulo».
---

# Capítulo revisado

Redline hacia **≥8/10**. No parche de gazapos. **No** sustituye el capítulo canónico (local ni `Capítulos`). Respuesta en **español**.

Fuente = bloque `### Para 8/10` de `analisis_cap{N}.md` (ítems `🎯8`). El resto de la lista accionable no se toca.

## Flujo

1. **Relato + cap.** Si viene de `chapter-editor`, ya lo sabe. Si falta, preguntar.
2. **Leer** `relatos/<relato>/analisis_cap{N}.md`. Si no existe → parar. Pedir `chapter-editor` primero.
3. **Extraer el contrato 8/10.** Completado: lista de ítems `🎯8` con ancla `>` + `→`, más `Elecciones` si las hay.
   - Hay `### Para 8/10` → usar esos números.
   - No hay (análisis viejo) → tomar de la lista accionable todo `🎯8`; si tampoco hay marca, tomar 🟡 + 🔴 de ritmo/personaje/mundo/hilos/magia/cierre. **No** tomar 🔴 de prosa/grama salvo que rompa inmersión. Avisar: «análisis sin 🎯8; inferí la barra».
   - Cero ítems → parar. «Nada para 8/10. No hay redline.»
4. **Leer el capítulo fuente** (mismo criterio que `chapter-editor`). Base = texto **actual**, post-corrección ortográfica si ya corrió.
5. **Aplicar cada ítem 🎯8** sobre una copia. Orden: de abajo a arriba. Completado: cada ítem en `aplicados` u `omitidos`. Tras aplicar, el texto propuesto debe poder puntuar **≥8/10** (ritmo, gente, lore de este cap, cierre). Si un omitido impide la barra, decirlo.
6. **Guardar** `relatos/<relato>/revision_cap{N}.md` (sobreescribir). Formato: «Fichero local».
7. **Espejar** con `guarda-analisis`, tipo `Capítulo revisado — Cap {N}`. Padre = fila `Análisis — Cap {N}` en `Revisiones`. Un toggle heading. No escribir en `Capítulos`. No tocar `Edición`.
8. **Decir** URL del padre, ítems aplicados/omitidos, elecciones tomadas, si la barra ≥8/10 queda cubierta, y que el cap canónico sigue igual.

## Qué aplicar

De cada ítem `🎯8`:

- `>` = ancla. Buscar el fragmento **exacto**. Cita amplia (`"[inicio...]...[...final]"`) = ese tramo entero.
- `→` = operación. Si trae texto nuevo, usar **ese**. Si describe el cambio, reescribir el ancla en la voz del autor: recortar, condensar, decidir lore — no un capítulo distinto.
- Varios `>` en el mismo ítem = todas las anclas.
- `Elecciones`: usar la opción del análisis. Si falta, elegir la que encaje con `contexto_global/` y anotarla.

**Omitir** (anotar, no inventar otro arreglo) si:

- el ancla no está (ya corregido, recortado o distinto);
- el ancla ya coincide con el `→`;
- el `→` dice no tocar (p. ej. «no borrar, no expandir»).

Centro = mejoras que suben nota (ritmo, gente, mundo, hilos, magia, cierre). Gazapo gramatical ya cazado por la corrección ortográfica: fuera, salvo que el análisis lo haya marcado `🎯8`.

No aplicar ítems sin `🎯8`. No «mejorar» frases vecinas. No reordenar escenas salvo que un `→` 🎯8 lo pida.

## Marcado

El texto que no cambia se copia tal cual.

| Cambio | Markup Notion |
|--------|----------------|
| Alta (texto nuevo o reescrito) | `<span color="red">…</span>` |
| Baja (texto que sale) | `<span color="gray">~~…~~</span>` |

Patrones:

- Sustitución corta: `…<span color="gray">~~ocurra~~</span><span color="red">ocurría</span>…`
- Frase o pasaje nuevo: `<span color="gray">~~viejo~~</span> <span color="red">nuevo</span>`
- Borrar / recortar: solo gris tachado. Sin alta.
- Partir / expandir / condensar: baja del tramo viejo + alta del nuevo (puede ser más de un párrafo).

Alta y baja **contiguas**. Pintar solo el delta, no el párrafo entero si cambió una palabra.

## Fichero local

```
# Capítulo revisado: [nombre del relato] — Capítulo [N]
**Barra:** ≥8/10 cubierta | no cubierta — [omitido que lo impide]
**🎯8:** [aplicados] / [total]
**Omitidos:** [lista corta, o «ninguno»]
**Elecciones:** [N → opción | ninguna]
---
**Leyenda:** <span color="red">alta</span> · <span color="gray">~~baja~~</span>
---
[capítulo entero, ya marcado]
```

El cuerpo tras el segundo `---` es el capítulo. Conservar párrafos, diálogos y saltos del fuente. Solo cambia el markup de los deltas.

## Notion

`guarda-analisis` sube el `.md` tal cual (spans incluidos, un tab por línea dentro del toggle). Clave: `Capítulo revisado — Cap {N}`. Overwrite si ya existe.

## No hacer

- Reescribir `capítulos/{N}.md` ni `contenido.md`.
- Parchear la página Notion de `Capítulos`.
- Meter el redline dentro del toggle `Edición`.
- Inventar 🎯8 que no estén en el análisis (ni en el fallback inferido).
- Conformarse con corregir 🔴 de prosa y dejar el ritmo/gente/lore igual.
- Envolver el capítulo en ` ```markdown `.

## Hook

`chapter-editor` la ejecuta **después** de espejar `Edición` y de la corrección ortográfica local. Esta skill no corre `chapter-editor`.
