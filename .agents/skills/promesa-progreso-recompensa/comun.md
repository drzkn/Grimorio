# PPR — reglas compartidas

Carpeta [.agents/skills/promesa-progreso-recompensa/](.). Origen: cap. «La trama» (Sanderson). Usar desde la orquestadora (`SKILL.md`) y desde `promesa/`, `progreso/`, `recompensa/`. Respuesta al usuario en **español**.

## Capas (no mezclar)

| Path | Qué es |
|------|--------|
| `<ruta>/promesas.md` | Canon local: promesas, progreso planificado y recompensas por hilo |
| Notion `Roadmap` + `<ruta>/sinopsis.md` | Plan de obra. `## Promesas` solo con confirmación explícita |
| `<ruta>/analisis_ppr.md` | Evaluación PPR del relato entero |
| `<ruta>/analisis_ppr_cap{N}.md` | Evaluación PPR del capítulo N |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Entrada: confirmar pilares y alcance

**Siempre** antes de grill o evaluar (salvo **modo delegado** desde la orquestadora: el foco y alcance ya vienen fijados).

`AskQuestion` en un solo formulario:

1. **Pilares** (`allow_multiple: true`): `Promesa`, `Progreso`, `Recompensa`. Enunciado: «¿Qué pilares quieres trabajar?». Si el mensaje o la skill de pilar sugerían algunos: «Has mencionado […]; confirma o marca otros».
2. **Alcance** (si no quedó claro): `Relato entero` | `Capítulo` (+ N si capítulo).
3. **Camino** (si no quedó claro): `Grill` (definir / afilar) | `Evaluar` (auditar texto escrito).

Sin ningún pilar marcado: repetir **una vez**. No asumir los tres.

Sesión:

- `foco` ⊆ {`promesa`, `progreso`, `recompensa`}, no vacío.
- `alcance` = `relato` | `cap {N}`.
- `camino` = `grill` | `evaluar`.

### Skill de pilar con varios pilares marcados

Si el usuario invocó `ppr-promesa` / `ppr-progreso` / `ppr-recompensa` (carpeta `promesa/` / `progreso` / `recompensa/`) y marca **más de un** pilar: delegar a orquestadora `promesa-progreso-recompensa` con ese foco y alcance; no continuar en la skill de pilar.

### Pilares fuera del foco

Leer de `promesas.md`, `sinopsis.md` o texto. No preguntar ni puntuar.

### Dependencias

Progreso y recompensa cuelgan de promesas definidas. Si `promesa` ∉ `foco` y no hay promesas en `promesas.md` ni deducibles de sinopsis/texto:

- Avisar.
- Ofrecer: añadir `promesa` al foco, skill `ppr-promesa` (`promesa/`) primero, o ronda mínima para fijar promesas necesarias.

Grill con varios pilares: frontera en orden **promesa → progreso → recompensa** (no progreso/recompensa de un hilo aún abierto en el grill).

## Semilla (grill)

Orden:

1. `<ruta>/promesas.md` si existe.
2. `sinopsis.md` tras volcar `Roadmap` (skill `sinopsis`; solo traer).
3. `contexto_global/`, caps del relato.
4. Mensaje del escritor si no hay local.
5. Sin semilla: una pregunta («pega premisa o qué prometes al lector») y parar.

Hechos escritos: buscar, no preguntar al escritor.

## Fuentes (evaluar)

- Cap: texto del cap (como `chapter-editor`: `capitulo_N.md`, `capN.md`, sección en `contenido.md`).
- Relato: caps disponibles + `contexto_global/` si existe.
- `promesas.md`, `sinopsis.md` si existen.
- `contexto_global/capitulos/<N>.md` cuando aplique.

Sin cita del texto o del plan, no hay hallazgo. No modificar `promesas.md` en evaluar sin permiso.

Propuesta ante desvío tipo Shadesmar: **preferir cambiar promesa** antes que reescribir todo el progreso.

## Formato ronda grill

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <recomendación desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

Frontera = decisiones abiertas cuyas previas están cerradas. Una ronda = frontera entera; «sí» acepta la recomendación. Frontera vacía → resumen (pilares del foco) → confirmación → persistir.

**Tope grill:** huecos que cambian compromisos con el lector. Reparto de caps: `sugerencia-capitulos`.

## Merge `promesas.md`

| Pilar en foco | Secciones / columnas que puede reescribir |
|---------------|-------------------------------------------|
| `promesa` | `## Tono`, `## Arcos de personaje`, `## Trama`, `## Anidamiento`; columnas Tipo promesa, Se abre en; filas nuevas de hilos |
| `progreso` | Columnas Progreso (hitos), Pasos atrás; `## Notas de riesgo` (riesgos de progreso) |
| `recompensa` | Columnas Recompensa (tipo), Se paga en, Estado; `## Notas de riesgo` (riesgos de pago) |

Si el fichero no existía: plantilla completa. Actualizar `Última actualización` y, tras confirmación del escritor, `Última confirmación`.

## Merge informe PPR

- Cap: `<ruta>/analisis_ppr_cap{N}.md`
- Relato: `<ruta>/analisis_ppr.md`

Reescribir solo `## Promesa`, `## Progreso`, `## Recompensa` de los pilares del foco; actualizar filas en `## Resumen de notas`. Resto intacto. Si no existía: plantilla completa; pilares no evaluados = `—` en resumen y sección mínima «No evaluado en esta pasada».

Tras evaluar: ejecutar skill `guarda-analisis` (clave `PPR — Cap {N}` o `PPR — Relato`).

## Volcado a sinopsis

Solo tras **grill**, si el foco incluía `promesa` o `recompensa` **y** hubo cambios en «se abre en» / «se paga en». Preguntar: «¿Vuelco las promesas a la sección Promesas de la sinopsis (Roadmap)?». Solo con **sí**: skill `sinopsis`, formato `- **[Hilo]:** se abre en … / se paga en … / estado`. Grill solo de `progreso` → no preguntar.

Skills `promesa/` y `recompensa/` pueden disparar esta pregunta en modo autónomo. La orquestadora, una sola vez al final.

## Plantilla `promesas.md`

```markdown
# Promesas: [nombre del relato]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## Tono
[Qué experiencia promete la presentación. Coherencia género/estilo.]

## Arcos de personaje
- **[Personaje]:** quiere / le falta / obstáculo / emblemático (sí|no) / arco previsto

## Trama
- **Paraguas:** [estructura visible]
- **Nuclear:** [lo que de verdad importa al lector]

## Anidamiento
[Corchetes: paraguas ⊃ argumental ⊃ personaje ⊃ subtramas. Qué cierra en qué tramo.]

## Hilos (promesa → progreso → recompensa)

| Hilo | Tipo promesa | Se abre en | Progreso (hitos) | Pasos atrás | Recompensa (tipo) | Se paga en | Estado |
|------|--------------|------------|------------------|-------------|-------------------|------------|--------|
| ... | tono / arco / trama | cap / acto | ... | ... | directa / expansión / sustitución | ... | abierta / en progreso / pagada / rota |

## Notas de riesgo
- [minipromesas, subtramas, sustitución…]
```

Estado del hilo: `abierta` | `en progreso` | `pagada` | `rota`.

## Plantilla informe PPR

```markdown
# PPR — [Relato | Cap N]

**Alcance:** relato | capítulo N
**Última evaluación:** YYYY-MM-DD

## Resumen de notas

| Pilar | Nota | Última evaluación |
|-------|------|-------------------|
| Promesa | — o N/10 | YYYY-MM-DD o — |
| Progreso | — o N/10 | YYYY-MM-DD o — |
| Recompensa | — o N/10 | YYYY-MM-DD o — |

## Promesa

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Progreso

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Recompensa

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...
```

## Modo delegado

La orquestadora fija `foco`, `alcance`, `camino`. La skill de pilar invocada en delegado:

- Lee su `teoria.md`.
- Aporta **rama del grill** (decisiones, frontera, riesgos) o **criterios de evaluación** cap/relato.
- No hace `AskQuestion`, no escribe ficheros, no llama `guarda-analisis`, no pregunta sinopsis.

## No hacer (todas las skills PPR)

- Copiar texto literal del libro fuente privado.
- Escribir en `Roadmap` / `sinopsis.md` sin confirmación explícita.
- Asumir pilares sin `AskQuestion` (salvo delegado).
- Repartir capítulos (`sugerencia-capitulos`).
- Inventar citas o promesas no presentes en texto/plan.

## Relación con otras skills

| Skill | Uso |
|-------|-----|
| `iniciar-relato` | Primero si falta relato activo |
| `sinopsis` | Roadmap; volcar `## Promesas` solo si el escritor confirma |
| `guarda-analisis` | Tras informe PPR local |
| `promesa-progreso-recompensa` | Orquestadora (`SKILL.md` en esta carpeta) si foco tiene 2–3 pilares |
| `chapter-editor` | Mismo criterio de localizar cap |
