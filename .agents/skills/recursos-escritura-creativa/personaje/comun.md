# Personaje — reglas compartidas

Carpeta [.agents/skills/recursos-escritura-creativa/personaje/](.). Origen: cap. «Cómo crear un personaje» (Sanderson). Usar desde la orquestadora (`SKILL.md`), `escalas/`, `motivacion/`, `limites/`. Respuesta al usuario en **español**.

Al persistir `personajes.md` o informes: skill `wikilinks`.

## Capas (no mezclar)

| Path | Qué es | Dueño |
|------|--------|-------|
| `<ruta>/personajes.md` | Canon de **uso**: escalas, motivo, frenos, POV, riesgos por personaje | Grill de esta familia |
| `<ruta>/esquema.md` `# Personajes` | Ficha de autor (presentación, arcos listados) | `ppr-trama`. Grill lee. Volcado solo con sí |
| `<ruta>/promesas.md` `## Arcos de personaje` | Promesa y anidamiento de arco | PPR. Grill lee. No reescribir desde aquí |
| `<ruta>/analisis_personajes.md` | Evaluación personaje del relato entero | Evaluar |
| `<ruta>/analisis_personajes_cap{N}.md` | Evaluación personaje del capítulo N | Evaluar |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Temas sensibles

Si el relato representa salud mental u otros colectivos vulnerables: investigar, fuentes primarias, lectores de prueba pagados si son expertos. No diagnosticar ni estereotipar en grill/evaluar.

## Entrada: confirmar pilares y alcance

**Siempre** antes de grill o evaluar (salvo **modo delegado** desde la orquestadora: el foco y alcance ya vienen fijados).

`AskQuestion` en un solo formulario:

1. **Pilares** (`allow_multiple: true`): `Escalas`, `Motivación`, `Límites`. Enunciado: «¿Qué pilares de personaje quieres trabajar?». Si el mensaje o la skill de pilar sugerían algunos: «Has mencionado […]; confirma o marca otros».
2. **Alcance** (si no quedó claro): `Relato entero` | `Capítulo` (+ N si capítulo).
3. **Camino** (si no quedó claro): `Grill` (definir / afilar) | `Evaluar` (auditar texto escrito).

Sin ningún pilar marcado: repetir **una vez**. No asumir los tres.

Sesión:

- `foco` ⊆ {`escalas`, `motivacion`, `limites`}, no vacío.
- `alcance` = `relato` | `cap {N}`.
- `camino` = `grill` | `evaluar`.

### Skill de pilar con varios pilares marcados

Si el usuario invocó `personaje-escalas` / `personaje-motivacion` / `personaje-limites` y marca **más de un** pilar: delegar a orquestadora `personaje` con ese foco y alcance; no continuar en la skill de pilar.

### Pilares fuera del foco

Leer de `personajes.md`, `esquema.md`, `promesas.md` o texto. No preguntar ni puntuar.

### Dependencias

`limites` y a menudo `motivacion` cuelgan de una mínima ficha (nombre, función en la historia). Si `motivacion` ∉ `foco` y no hay motivo en `personajes.md` ni en `# Personajes` de `esquema.md`:

- Avisar.
- Ofrecer: añadir `motivacion` al foco, skill `personaje-motivacion` primero, o ronda mínima para fijar motivo + objetivo de 1–2 personajes del foco.

Grill con varios pilares: frontera en orden **escalas → motivacion → limites**.

## Semilla (grill)

Orden:

1. `<ruta>/personajes.md` si existe.
2. `<ruta>/esquema.md` `# Personajes` si existe.
3. `<ruta>/promesas.md` si existe (solo traer arcos).
4. `contexto_global/`, caps del relato.
5. Mensaje del escritor si no hay local.
6. Sin semilla: una pregunta («¿quién es el foco, qué ya sabes de motivos y arco?») y parar.

Hechos escritos: buscar, no preguntar al escritor.

## Fuentes (evaluar)

- Cap: texto del cap (como `chapter-editor`: `capitulo_N.md`, `capN.md`, sección en `contenido.md`). Cortar en el `---` de `## Relacionado`.
- Relato: caps disponibles + `contexto_global/` si existe.
- `personajes.md`, `esquema.md`, `promesas.md`, `sinopsis.md` si existen.
- `contexto_global/capitulos/<N>.md` cuando aplique.

Sin cita del texto o del plan (`personajes.md` / `esquema.md`), no hay hallazgo. No modificar `personajes.md` en evaluar sin permiso.

## Formato ronda grill

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <recomendación desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

Frontera = decisiones abiertas cuyas previas están cerradas. Una ronda = frontera entera; «sí» acepta la recomendación. Frontera vacía → resumen (pilares del foco) → confirmación → persistir.

**Tope grill:** huecos que cambian a quién apoya el lector, por qué, y dónde duele el personaje. Prosa: `chapter-editor`. Arcos y promesas: PPR. Escaleta: `sugerencia-capitulos`. Ficha enciclopédica de autor: `ppr-trama`.

## Merge `personajes.md`

Por personaje relevante del foco: reescribir solo las líneas de los pilares en juego:

| Pilar en foco | Campos que puede reescribir |
|---------------|----------------------------|
| `escalas` | `Función lectora`, `Escalas` |
| `motivacion` | `Objetivo`, `Motivo`, `Querer / necesitar`, `Motivos en conflicto`, `Villano / antagonista` |
| `limites` | `Defecto`, `Desventaja`, `Limitación`, `Rareza anclada` |

Cualquier pilar puede añadir filas en `## Riesgos`. Campos transversales (`POV`, `Antes de la trama`) en grill de varios pilares o si el escritor los fijó en semilla.

Si el fichero no existía: plantilla completa. Actualizar `Última actualización` y, tras confirmación del escritor, `Última confirmación`.

## Merge informe personaje

- Cap: `<ruta>/analisis_personajes_cap{N}.md`
- Relato: `<ruta>/analisis_personajes.md`

Reescribir solo `## Escalas`, `## Motivación`, `## Límites` de los pilares del foco; actualizar filas en `## Resumen de notas`. Resto intacto. Si no existía: plantilla completa; pilares no evaluados = `—` en resumen y sección mínima «No evaluado en esta pasada».

Cabecera `**Fuente:**` según `wikilinks`. Tras evaluar: ejecutar skill `guarda-analisis` (clave `Personajes — Cap {N}` o `Personajes — Relato`).

## Volcado a esquema

Solo tras **grill**, si hubo **cambios en fichas** de personajes (presentación, motivo, arco listado) en personajes tocados. Preguntar: «¿Vuelco las fichas a `# Personajes` del esquema?». Solo con **sí**: editar `esquema.md` `# Personajes` (definiciones de autor, no prosa del capítulo). Grill que no alteró fichas → no preguntar.

La orquestadora hace la pregunta una sola vez al final.

## Pregunta PPR

Tras grill confirmado: «¿Siguiente paso?» — **PPR** de arcos (`recursor-escritura-creativa`) | **parar**. Una sola pregunta junto al volcado esquema o después.

## Plantilla `personajes.md`

```markdown
# Personajes: [nombre del relato]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## [Nombre]
- **Función lectora:** empatía | apoyo | progreso | emblemático
- **Escalas:** simpatía [inicio → movimiento]; resolución […]; capacidad [campo de esta trama: …]
- **Objetivo:** …
- **Motivo:** … (permanece aunque el objetivo cambie)
- **Querer / necesitar:** …
- **Motivos en conflicto:** …
- **Villano / antagonista:** … (si aplica)
- **Defecto:** …
- **Desventaja:** …
- **Limitación:** …
- **Rareza anclada:** …
- **POV:** significativo | sabor | ninguno
- **Antes de la trama:** …

## Riesgos
- [gorila en cabina, motivación única estática, capacidad sin fricción, rareza suelta, papel prefabricado…]
```

## Plantilla informe personaje

```markdown
# Personajes — [Relato | Cap N]

**Fuente:** [[<relato>/capítulos/N|Capítulo N]] · [[<relato>/contexto_global/capitulos/N|Nota cap N]]
**Alcance:** relato | capítulo N
**Última evaluación:** YYYY-MM-DD

## Resumen de notas

| Pilar | Nota | Última evaluación |
|-------|------|-------------------|
| Escalas | — o N/10 | YYYY-MM-DD o — |
| Motivación | — o N/10 | YYYY-MM-DD o — |
| Límites | — o N/10 | YYYY-MM-DD o — |

## Escalas

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Motivación

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Límites

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...
```

Relato entero: `**Fuente:**` lista de caps leídos (mismo formato). Sin nota de cap → omitir ese enlace.

## Modo delegado

La orquestadora fija `foco`, `alcance`, `camino`. La skill de pilar invocada en delegado:

- Lee su `teoria.md`.
- Aporta **rama del grill** (decisiones, frontera, riesgos) o **criterios de evaluación** cap/relato.
- No hace `AskQuestion`, no escribe ficheros, no llama `guarda-analisis`, no pregunta esquema.

## No hacer (todas las skills personaje)

- Copiar texto literal del libro fuente privado.
- Reescribir `promesas.md` o grillar anidamiento PPR.
- Escribir en `esquema.md` `# Personajes` sin confirmación explícita.
- Asumir pilares sin `AskQuestion` (salvo delegado).
- Repartir capítulos (`sugerencia-capitulos`).
- Inventar citas o motivaciones no presentes en texto/plan.
- Grillar defecto/limitación/coste del **sistema de magia** → familia `leyes-magia`. Coincidencia persona/magia: una línea en `## Riesgos`.
- Grillar arco de promesa completo → PPR.

## Relación con otras skills

| Skill | Uso |
|-------|-----|
| `iniciar-relato` | Primero si falta relato activo |
| `ppr-trama` | Fichas `# Personajes` en `esquema.md` |
| `recursor-escritura-creativa` | Tras grill, si el escritor confirma PPR |
| `guarda-analisis` | Tras informe personaje local |
| `personaje` | Orquestadora si foco tiene 2–3 pilares |
| `chapter-editor` | Mismo criterio de localizar cap; no sustituye esta pasada |
| `leyes-magia` | Sistema de magia; no duplicar restricciones de poder |
| `mundo` | Ambientación; no grillar arco ni ficha de persona |