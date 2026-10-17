---
name: sugerencia-capitulos
description: >-
  Reparte el plan de la obra en capítulos y marca el ritmo (guía local
  sugerencia_capitulos.md). Parte de la sinopsis vigente (Notion Roadmap).
  No toca el canon. Úsalo cuando el usuario diga "sugerencia de capítulos",
  "reparto de capítulos", "distribución de la historia", "ritmo de capítulos",
  "sugerencia-capitulos", o tras un grill de sinopsis si pide el reparto.
---

# Sugerencia de capítulos

Guía para **escribir**: qué podría tratar cada capítulo y cómo sube o respira el ritmo. **No es canon.** El plan es Notion `Roadmap` / `<ruta>/sinopsis.md` (skill `sinopsis`).

Respuesta al usuario en **español**.

## Capas (no mezclar)

| Path | Qué es |
|------|--------|
| Notion `Roadmap` + `<ruta>/sinopsis.md` | Plan. Esta skill **lee**, no escribe |
| `<ruta>/sugerencia_capitulos.md` | Guía. Solo local. Esta skill la escribe |
| `capítulos/` y notas | Caps ya escritos: anclan números. No se renumeran |

`<ruta>` / `nombre` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Flujo

1. **Relato activo**: skill `iniciar-relato`.
2. **Plan vigente**: seguir skill `sinopsis` solo para traer `Roadmap` → `sinopsis.md` si hay cuerpo, y leer esa copia. Si Notion no responde: parar y decirlo. Si no hay plan (Roadmap vacío y no hay local): una línea — «corre `sinopsis` primero» — y parar. No grillar el storyboard aquí.
   - **Oficio**: skill `oficio`, cargar `trama` (progreso, ritmo, ausencias largas de una trama).
3. **Caps ya escritos**: glob `<ruta>/capítulos/` (o `capitulos/`). Esos números quedan `anclado`.
4. **Huecos de llegada**: donde la sinopsis tiene dos beats y ningún tramo entre ellos. Una ruta por hueco (cuántos caps, función, si el ritmo sube / sostiene / respira). Destino = el beat ya cerrado. Hecho nuevo de trama **no** entra en `Roadmap`.
5. Si el escritor pide afinar el reparto: rondas cortas (formato grill), **solo** ritmo y corte de caps. No desenlace, no destino de arco, no promesas del plan.
6. Escribir `<ruta>/sugerencia_capitulos.md` (plantilla abajo). Sobreescribir si existe.
7. Informar: ruta, caps anclados vs sugeridos, puentes. 2–4 líneas. No volcar el fichero entero.

## Plantilla

```markdown
# Sugerencia de capítulos: [nombre]

**Basada en:** Notion Roadmap ([fecha de confirmación])
**Última actualización:** YYYY-MM-DD

Guía para escribir. El plan es Notion Roadmap.

## Ritmo
[Cómo sube y baja la obra. Dónde aprieta, dónde respira, y qué tramo es un puente entre dos beats que el escritor ya tiene.]

## Capítulos
| Cap | Función | Trata | Ritmo | Origen |
|-----|---------|-------|-------|--------|
| 1 | apertura | beat 1 | engancha | anclado |
| 4 | puente | del beat 2 al beat 5 | sostiene | sugerido |
| 8 | pago | beat 9, promesa X | cae | anclado |

## Puentes
- **Caps [A]–[B]:** entre [beat conocido] y [beat conocido]. Ruta: [qué puede tratar cada capítulo de ese hueco para llegar al beat que la sinopsis ya fijó].
```

Función: `apertura` | `desarrollo` | `giro` | `puente` | `respiro` | `pago`.

Origen: `anclado` (beat ya decidido o capítulo ya escrito) | `sugerido` (ruta para un vacío).

Capítulo N ya escrito → esa fila usa ese número y resume lo que ya trata. No renumerar el pasado. Puente solo donde hay dos beats y ningún tramo entre ellos.

## No hacer

- Escribir `Roadmap` o `sinopsis.md`.
- Inventar desenlace o beats. El destino ya está en la sinopsis.
- Usar esta guía como vara de contraste editorial (`chapter-editor` no la lee).
- Correr si no hay plan. Mandar a `sinopsis`.

## Relación con otras skills

| Skill | Qué hacer |
|-------|-----------|
| `iniciar-relato` | Primero. Relato activo |
| `sinopsis` | Fuente del plan. Si falta, parar |
| `chapter-editor` | No llama esta skill. No contrasta contra la guía |
| `chapter-reader` / `fantasy-reader` | No leen `sugerencia_capitulos.md` |
