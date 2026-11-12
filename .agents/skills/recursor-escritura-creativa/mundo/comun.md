# Mundo — reglas compartidas

Carpeta [.agents/skills/recursor-escritura-creativa/mundo/](.). Origen: cap. «Cómo crear un mundo» (Sanderson). Usar desde la orquestadora (`SKILL.md`), `entrega/`, `construccion/`, `consistencia/`. Respuesta al usuario en **español**.

Al persistir `mundo.md` o informes: skill `wikilinks`.

## Capas (no mezclar)

| Path | Qué es | Dueño |
|------|--------|-------|
| `<ruta>/mundo.md` | Canon de **uso**: presupuesto, elementos, ramificaciones, curva, reglas internas, misterio | Grill de esta familia |
| `<ruta>/esquema.md` `# Ambientación` | Enciclopedia de autor (magia, mundo físico, cultura) | `ppr-trama`. Grill lee. Volcado solo con sí |
| `<ruta>/contexto.md` | Reglas ya canon del autor | Semilla de **solo lectura**. `build-context` no se toca |
| `<ruta>/analisis_mundo.md` | Evaluación mundo del relato entero | Evaluar |
| `<ruta>/analisis_mundo_cap{N}.md` | Evaluación mundo del capítulo N | Evaluar |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Entrada: confirmar pilares y alcance

**Siempre** antes de grill o evaluar (salvo **modo delegado** desde la orquestadora: el foco y alcance ya vienen fijados).

`AskQuestion` en un solo formulario:

1. **Pilares** (`allow_multiple: true`): `Entrega`, `Construcción`, `Consistencia`. Enunciado: «¿Qué pilares de mundo quieres trabajar?». Si el mensaje o la skill de pilar sugerían algunos: «Has mencionado […]; confirma o marca otros».
2. **Alcance** (si no quedó claro): `Relato entero` | `Capítulo` (+ N si capítulo).
3. **Camino** (si no quedó claro): `Grill` (definir / afilar) | `Evaluar` (auditar texto escrito).

Sin ningún pilar marcado: repetir **una vez**. No asumir los tres.

Sesión:

- `foco` ⊆ {`entrega`, `construccion`, `consistencia`}, no vacío.
- `alcance` = `relato` | `cap {N}`.
- `camino` = `grill` | `evaluar`.

### Skill de pilar con varios pilares marcados

Si el usuario invocó `mundo-entrega` / `mundo-construccion` / `mundo-consistencia` y marca **más de un** pilar: delegar a orquestadora `mundo` con ese foco y alcance; no continuar en la skill de pilar.

### Pilares fuera del foco

Leer de `mundo.md`, `esquema.md`, `contexto.md` o texto. No preguntar ni puntuar.

### Dependencias

Entrega y consistencia cuelgan de un mundo mínimo (qué existe, en qué se gasta presupuesto). Si `construccion` ∉ `foco` y no hay presupuesto/elementos en `mundo.md` ni `# Ambientación` en `esquema.md` ni `contexto.md`:

- Avisar.
- Ofrecer: añadir `construccion` al foco, skill `mundo-construccion` primero, o ronda mínima para fijar presupuesto y 1–3 elementos.

Grill con varios pilares: frontera en orden **construccion → consistencia → entrega**.

## Semilla (grill)

Orden:

1. `<ruta>/mundo.md` si existe.
2. `<ruta>/esquema.md` `# Ambientación` si existe.
3. `<ruta>/contexto.md` si existe (solo lectura).
4. `sinopsis.md` tras volcar `Roadmap` (skill `sinopsis`; solo traer).
5. `contexto_global/`, caps del relato.
6. Mensaje del escritor si no hay local.
7. Sin semilla: una pregunta («pega premisa, subgénero y qué del mundo ya está decidido») y parar.

Hechos escritos: buscar, no preguntar al escritor.

## Fuentes (evaluar)

- Cap: texto del cap (como `chapter-editor`: `capitulo_N.md`, `capN.md`, sección en `contenido.md`). Cortar en el `---` de `## Relacionado`.
- Relato: caps disponibles + `contexto_global/` si existe.
- `mundo.md`, `esquema.md`, `contexto.md`, `sinopsis.md` si existen.
- `contexto_global/capitulos/<N>.md` cuando aplique.

Sin cita del texto o del plan (`mundo.md` / `esquema.md`), no hay hallazgo. No modificar `mundo.md` en evaluar sin permiso.

## Formato ronda grill

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <recomendación desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

Frontera = decisiones abiertas cuyas previas están cerradas. Una ronda = frontera entera; «sí» acepta la recomendación. Frontera vacía → resumen (pilares del foco) → confirmación → persistir.

**Tope grill:** huecos que cambian cómo el lector vive el mundo (presupuesto, curva, reglas internas, misterio). Enciclopedia de autor: `ppr-trama` / `esquema.md`. Reparto de caps: `sugerencia-capitulos`.

## Merge `mundo.md`

| Pilar en foco | Secciones que puede reescribir |
|---------------|--------------------------------|
| `construccion` | `## Presupuesto`, `## Física`, `## Cultural`, `## Ramificaciones`; `## Riesgos` (construcción) |
| `consistencia` | `## Consistencia`, `## Misterio`; `## Riesgos` (consistencia) |
| `entrega` | `## Entrega`; `## Riesgos` (entrega). Puede anotar en `## Misterio` solo epígrafes / dosificación |

Si el fichero no existía: plantilla completa. Actualizar `Última actualización` y, tras confirmación del escritor, `Última confirmación`.

## Merge informe mundo

- Cap: `<ruta>/analisis_mundo_cap{N}.md`
- Relato: `<ruta>/analisis_mundo.md`

Reescribir solo `## Entrega`, `## Construcción`, `## Consistencia` de los pilares del foco; actualizar filas en `## Resumen de notas`. Resto intacto. Si no existía: plantilla completa; pilares no evaluados = `—` en resumen y sección mínima «No evaluado en esta pasada».

Cabecera `**Fuente:**` según `wikilinks`. Tras evaluar: ejecutar skill `guarda-analisis` (clave `Mundo — Cap {N}` o `Mundo — Relato`).

## Volcado a esquema

Solo tras **grill**, si el foco incluía `construccion` **y** hubo cambios en Presupuesto / Física / Cultural / Ramificaciones. Preguntar: «¿Vuelco los elementos de uso a `# Ambientación` del esquema?». Solo con **sí**: editar `esquema.md` sección `# Ambientación` (Magia / Mundo físico / Cultura) con definiciones de autor, no narración. Grill solo de `entrega` o `consistencia` → no preguntar.

Skills `construccion/` pueden disparar esta pregunta en modo autónomo. La orquestadora, una sola vez al final.

## Plantilla `mundo.md`

```markdown
# Mundo: [nombre del relato]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## Presupuesto
- **Subgénero:** [épica / urbana / grimdark / …]
- **Puntos:** [pocos | medios | muchos]
- **Ganchos en los que se gasta:** [1–3 elementos]

## Entrega
- **Curva:** [suave | media | muro] / público [infantil | juvenil | adulto]
- **Apertura:** [deseo concreto del personaje; qué del mundo hace falta para ese acto]
- **Canal:** [ojos del personaje | aprendiz/Watson | epígrafes de refuerzo | …]
- **Pirámide:** [qué queda abajo (concreto) antes de explicar sistemas]

## Física
- [elemento]: [qué existe aunque no hubiera gente]

## Cultural
- [elemento]: [qué aportan los seres pensantes]

## Ramificaciones
- [gancho] → [flora/fauna / magia / gobierno / religión / economía / tabú / moda]

## Consistencia
- **Interna:** [regla que el lector puede predecir]
- **Externa:** [qué del mundo real / género / mitología se respeta o se tuerce]
- **Coste si se tuerce:** [escena que graba la excepción]

## Misterio
- **Sabe el POV:** …
- **Hueco iluminado / disonancia:** …
- **No va en epígrafe (carga de trama):** …

## Riesgos
- [constructor de mundos, volcado, doncella-mayordomo, iceberg macizo, consistencia que choca con expectativa…]
```

## Plantilla informe mundo

```markdown
# Mundo — [Relato | Cap N]

**Fuente:** [[<relato>/capítulos/N|Capítulo N]] · [[<relato>/contexto_global/capitulos/N|Nota cap N]]
**Alcance:** relato | capítulo N
**Última evaluación:** YYYY-MM-DD

## Resumen de notas

| Pilar | Nota | Última evaluación |
|-------|------|-------------------|
| Entrega | — o N/10 | YYYY-MM-DD o — |
| Construcción | — o N/10 | YYYY-MM-DD o — |
| Consistencia | — o N/10 | YYYY-MM-DD o — |

## Entrega

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Construcción

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Consistencia

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

## No hacer (todas las skills mundo)

- Copiar texto literal del libro fuente privado.
- Reescribir `contexto.md` o fusionar `build-context`.
- Escribir en `esquema.md` `# Ambientación` sin confirmación explícita.
- Asumir pilares sin `AskQuestion` (salvo delegado).
- Repartir capítulos (`sugerencia-capitulos`).
- Inventar citas o reglas de mundo no presentes en texto/plan.
- Grillar magia como sistema de leyes → familia `leyes-magia`. Aquí solo ambientación ligada (presupuesto, ramificación, cómo se entrega).

## Relación con otras skills

| Skill | Uso |
|-------|-----|
| `iniciar-relato` | Primero si falta relato activo |
| `ppr-trama` | Enciclopedia `# Ambientación` en `esquema.md` |
| `guarda-analisis` | Tras informe mundo local |
| `mundo` | Orquestadora si foco tiene 2–3 pilares |
| `chapter-editor` | Mismo criterio de localizar cap; no sustituye esta pasada |
| `build-context` | No invocar; `contexto.md` solo semilla |
| `leyes-magia` | Sistemas de magia (leyes 0–3); no duplicar aquí |
