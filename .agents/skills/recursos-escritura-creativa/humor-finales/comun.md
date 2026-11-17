# Humor y finales — reglas compartidas

Carpeta [.agents/skills/recursos-escritura-creativa/humor-finales/](.). Origen: cap. «Humor, finales y revisiones» (Sanderson). Usar desde la orquestadora (`SKILL.md`), `humor/`, `finales/`, `revisiones/`. Respuesta al usuario en **español**.

Al persistir `humor-finales.md`, `revision.md` o informes: skill `wikilinks`.

## Capas (no mezclar)

| Path | Qué es | Dueño |
|------|--------|-------|
| `<ruta>/humor-finales.md` | Canon: humor planificado y mapa de cierre | Grill `humor` y/o `finales` |
| `<ruta>/revision.md` | Guía jerárquica, versión objetivo, fases alfa/beta | Grill `revisiones` |
| `<ruta>/promesas.md` | Tono, arcos, pagos | PPR. Solo lectura aquí |
| `<ruta>/sinopsis.md`, `<ruta>/esquema.md` | Plan | Solo lectura |
| `<ruta>/analisis_humor_finales.md` | Evaluación humor/finales relato | Evaluar humor o finales |
| `<ruta>/analisis_humor_finales_cap{N}.md` | Evaluación humor/finales cap N | Evaluar cap |
| `<ruta>/analisis_revision.md` | Evaluación del proceso de revisión | Evaluar `revisiones` |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Entrada: confirmar pilares y alcance

**Siempre** antes de grill o evaluar (salvo **modo delegado** desde la orquestadora).

`AskQuestion` en un solo formulario:

1. **Pilares** (`allow_multiple: true`): `Humor`, `Finales`, `Revisiones`. Enunciado: «¿Qué pilares quieres trabajar?».
2. **Alcance** (si no quedó claro): `Relato entero` | `Capítulo` (+ N si capítulo). **Revisiones evaluar:** por defecto relato; si el escritor pide cap, limitar a retoques listados.
3. **Camino** (si no quedó claro): `Grill` | `Evaluar`.

Sin ningún pilar marcado: repetir **una vez**.

Sesión:

- `foco` ⊆ {`humor`, `finales`, `revisiones`}, no vacío.
- `alcance` = `relato` | `cap {N}`.
- `camino` = `grill` | `evaluar`.

### Skill de pilar con varios pilares marcados

Si el usuario invocó un skill de pilar y marca **más de un** pilar: delegar a orquestadora `humor-finales` con ese foco y alcance.

### Pilares fuera del foco

Leer de `humor-finales.md`, `revision.md`, `promesas.md` o texto. No preguntar ni puntuar.

### Dependencias

`finales` en grill: avisar si no hay `promesas.md`, `sinopsis.md` ni arcos deducibles del texto. Ofrecer: añadir `ppr-promesa` / PPR, o ronda mínima de tramas en grill.

Grill con varios pilares: frontera **humor → finales → revisiones** (revisiones no reabre humor/finales ya confirmados en la sesión).

## Semilla (grill)

Orden:

1. `<ruta>/humor-finales.md` si existe.
2. `<ruta>/revision.md` si existe (`revisiones` en foco).
3. `<ruta>/promesas.md`, `<ruta>/sinopsis.md`, `<ruta>/esquema.md`.
4. `contexto_global/`, caps del relato.
5. Mensaje del escritor.
6. Sin semilla: una pregunta según pilar («¿qué función tiene el humor?» / «¿cómo imaginas el cierre?» / «¿en qué versión estás del borrador?») y parar.

Hechos escritos: buscar, no preguntar al escritor.

## Fuentes (evaluar)

- Cap: texto del cap (como `chapter-editor`: `capitulo_N.md`, `capN.md`, sección en `contenido.md`).
- Relato: caps + `contexto_global/`.
- `humor-finales.md`, `revision.md`, `promesas.md` si existen.

Sin cita del texto o del plan, no hay hallazgo. No modificar canon en evaluar sin permiso.

## Formato ronda grill

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <recomendación desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

Frontera vacía → resumen → confirmación → persistir.

**Tope grill:** cambia tono cómico global, mapa de clímax, muertes con peso dramático, o fases de revisión del manuscrito. Prosa de cap: `chapter-editor`. Promesas completas: PPR.

## Merge `humor-finales.md`

| Pilar en foco | Secciones |
|---------------|-----------|
| `humor` | `## Humor` (función, tipos, personajes clave, gags) |
| `finales` | `## Finales` (tipo cierre, curvas, punto A/B, giros, muertes, presagios) |

Si no existía: plantilla abajo. Actualizar `Última actualización` y `Última confirmación` tras confirmación.

## Merge `revision.md`

Solo pilar `revisiones`. Secciones: `## Versión objetivo`, `## Guía de revisión` (lista jerárquica), `## Siguiente fase` (alfa/beta/prosa), `## Riesgos de proceso`.

## Merge informe humor/finales

- Cap: `analisis_humor_finales_cap{N}.md`
- Relato: `analisis_humor_finales.md`

Reescribir solo `## Humor` y/o `## Finales` del foco. Cabecera `**Fuente:**` según `wikilinks`. Tras evaluar: `guarda-analisis` (`Humor y finales — Cap {N}` o `Humor y finales — Relato`).

## Merge informe revisiones

Solo `analisis_revision.md`. Clave Notion: `Revisión — Relato`. Tras evaluar: `guarda-analisis`.

## Pregunta PPR

Tras grill de `finales` que alteró cierre o pagos: «¿Siguiente paso?» — **PPR** (`recursor-escritura-creativa` / `ppr-recompensa`) | **parar**. Una pregunta al final.

## Plantilla `humor-finales.md`

```markdown
# Humor y finales: [nombre del relato]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## Humor
- **Función en la obra:** …
- **Tonos y riesgos:** …
- **Caídas / parejas:** …
- **Yuxtaposiciones que marcan obra:** …
- **Gags recurrentes:** …
- **Métodos mezclados:** personaje | relación | textual

## Finales
- **Tipo de cierre:** avalancha | tragedia | agridulce | …
- **Curvas por personaje:** …
- **Punto A (avalancha) / B (arcos menores):** …
- **Entrelazado o escalonado:** …
- **Giros del acto final:** …
- **Muertes y propósito:** …
- **Presagios:** …

## Riesgos
- …
```

## Plantilla `revision.md`

```markdown
# Revisión: [nombre del relato]

**Última actualización:** YYYY-MM-DD
**Versión actual aproximada:** 1.0 | 2.0 | …

## Versión objetivo
…

## Guía de revisión
1. [libro / subtrama]
2. …
- …

## Siguiente fase
Alfa | Beta | Prosa 5.0 | …

## Riesgos de proceso
- …
```

## Plantilla informe humor/finales

```markdown
# Humor y finales — [Relato | Cap N]

**Fuente:** …
**Alcance:** relato | capítulo N
**Última evaluación:** YYYY-MM-DD

## Resumen de notas

| Pilar | Nota | Última evaluación |
|-------|------|-------------------|
| Humor | — o N/10 | … |
| Finales | — o N/10 | … |

## Humor
**Evaluado:** … | **Nota:** N/10
### Hallazgos
### Propuestas

## Finales
**Evaluado:** … | **Nota:** N/10
### Hallazgos
### Propuestas
```

## Plantilla informe revisiones

```markdown
# Revisión — Relato

**Fuente:** `revision.md`, notas del escritor, caps leídos
**Última evaluación:** YYYY-MM-DD

## Diagnóstico del proceso
…

## Hallazgos
…

## Propuesta de siguiente pasada
…
```

## Modo delegado

La orquestadora fija `foco`, `alcance`, `camino`. La skill de pilar invocada:

- Lee su `teoria.md`.
- Aporta rama del grill o criterios de evaluación.
- No hace `AskQuestion`, no escribe ficheros, no llama `guarda-analisis`.

## No hacer (todas las skills humor-finales)

- Copiar texto literal del libro fuente privado.
- Reescribir `promesas.md` desde grill de finales.
- Grillar tipos de pago PPR solos → `ppr-recompensa`.
- Sustituir `chapter-editor` o `caracterizacion-dialogo` salvo una línea de enlace.
- Inventar citas o chistes no presentes en texto/plan.
- Evaluar revisiones con nota de cap como clímax narrativo (proceso = relato).

## Relación con otras skills

| Skill | Uso |
|-------|-----|
| `iniciar-relato` | Primero si falta relato activo |
| `humor-finales` | Orquestadora si foco tiene 2–3 pilares |
| `recursor-escritura-creativa` / `ppr-recompensa` | Promesas y pagos |
| `caracterizacion-dialogo` | Forma del diálogo |
| `personaje` | Escalas, muerte, partir personaje |
| `guarda-analisis` | Tras informe local |
| `chapter-editor` | Prosa de capítulo |