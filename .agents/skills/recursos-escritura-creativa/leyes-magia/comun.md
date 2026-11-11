# Leyes de la magia — reglas compartidas

Carpeta [.agents/skills/recursor-escritura-creativa/leyes-magia/](.). Origen: cap. «Las leyes de la magia» (Sanderson). Pack del curso: carpeta padre `recursor-escritura-creativa/`. Usar desde la orquestadora (`SKILL.md`), `cero/`, `primera/`, `segunda/`, `tercera/`. Respuesta al usuario en **español**.

Las cuatro leyes son **herramientas**, no normas. Si matan la historia, se descartan.

## Capas (no mezclar)

| Path | Qué es |
|------|--------|
| `<ruta>/sistema_magia.md` | Canon local del sistema: imagen, poderes, defectos, espectro, profundidad |
| `<ruta>/analisis_magia.md` | Evaluación de magia del relato entero |
| `<ruta>/analisis_magia_cap{N}.md` | Evaluación de magia del capítulo N |
| `<ruta>/promesas.md` | PPR. Esta pack **no** lo escribe |
| `<ruta>/esquema.md` | Esquema de trama. Esta pack **no** lo escribe |
| Notion `Roadmap` + `<ruta>/sinopsis.md` | Plan de obra. Esta pack **no** lo escribe |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

Grill con alcance capítulo: el canon sigue siendo **el del relato**; el cap es evidencia. No hay un sistema de magia por capítulo.

## Entrada: confirmar leyes y alcance

**Siempre** antes de grill o evaluar (salvo **modo delegado** desde la orquestadora: el foco y alcance ya vienen fijados).

`AskQuestion` en un solo formulario:

1. **Leyes** (`allow_multiple: true`): `Ley cero`, `Primera`, `Segunda`, `Tercera`. Enunciado: «¿Qué leyes quieres trabajar?». Si el mensaje o la skill de pilar sugerían algunas: «Has mencionado […]; confirma o marca otras». Petición genérica de pulir el sistema: **proponer las cuatro**, sin asumirlas si no marcan.
2. **Alcance** (si no quedó claro): `Relato entero` | `Capítulo` (+ N si capítulo).
3. **Camino** (si no quedó claro): `Grill` (definir / afilar) | `Evaluar` (auditar texto escrito).

Sin ninguna ley marcada: repetir **una vez**. No asumir las cuatro.

Sesión:

- `foco` ⊆ {`cero`, `primera`, `segunda`, `tercera`}, no vacío.
- `alcance` = `relato` | `cap {N}`.
- `camino` = `grill` | `evaluar`.

### Skill de pilar con varias leyes marcadas

Si el usuario invocó `magia-ley-cero` / `magia-primera-ley` / `magia-segunda-ley` / `magia-tercera-ley` (carpeta `cero/` / `primera/` / `segunda/` / `tercera/`) y marca **más de una** ley: delegar a orquestadora `leyes-magia` con ese foco y alcance; no continuar en la skill de pilar.

### Leyes fuera del foco

Leer de `sistema_magia.md`, `sinopsis.md` o texto. No preguntar ni puntuar.

### Dependencias

Segunda, Primera y Tercera cuelgan de una imagen o un poder. Si `cero` ∉ `foco` y no hay imagen ni poder en `sistema_magia.md` ni en el texto:

- Avisar.
- Ofrecer: añadir `cero` al foco, skill `magia-ley-cero` (`cero/`) primero, o ronda mínima para fijar la imagen.

Grill con varias leyes: frontera en orden **cero → segunda → primera → tercera** (no espectro/conflictos de un sistema aún abierto en imagen o restricciones).

## Semilla (grill)

Orden:

1. `<ruta>/sistema_magia.md` si existe.
2. `<ruta>/esquema.md` si existe.
3. `sinopsis.md` (Roadmap vía skill `sinopsis` si hace falta; **solo traer**, no escribir).
4. `contexto_global/`, caps del relato.
5. Mensaje del escritor si no hay local.
6. Sin semilla: una pregunta («pega el poder o la imagen») y parar.

Hechos escritos: buscar, no preguntar al escritor.

## Fuentes (evaluar)

- Cap: texto del cap (como `chapter-editor`: `capitulo_N.md`, `capN.md`, sección en `contenido.md`).
- Relato: caps disponibles + `contexto_global/` si existe.
- `sistema_magia.md`, `sinopsis.md`, `esquema.md` si existen.
- `contexto_global/capitulos/<N>.md` cuando aplique.

Sin cita del texto o del plan, no hay hallazgo. No modificar `sistema_magia.md` en evaluar sin permiso.

## Formato ronda grill

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <recomendación desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

Frontera = decisiones abiertas cuyas previas están cerradas. Una ronda = frontera entera; «sí» acepta la recomendación. Frontera vacía → resumen (leyes del foco) → confirmación → persistir.

**Tope grill:** huecos que cambian qué puede hacer la magia, a qué precio, qué entiende el lector y qué no se añade. Prosa, arcos de personaje y reparto de capítulos: fuera (PPR y `sugerencia-capitulos`). Si un defecto de la magia coincide con el del personaje, una línea en `## Notas de riesgo`, no un grill de arco.

## Merge `sistema_magia.md`

| Ley en foco | Secciones que puede reescribir |
|-------------|-------------------------------|
| `cero` | `## Impresionante`; semilla de `## Poderes` |
| `segunda` | `## Defectos`, `## Limitaciones`, `## Costes` |
| `primera` | `## Espectro`, `## Conflictos que la magia puede cerrar` |
| `tercera` | `## Profundidad` |
| cualquiera | sus riesgos en `## Notas de riesgo` |

Si el fichero no existía: plantilla completa. Actualizar `Última actualización` y, tras confirmación del escritor, `Última confirmación`.

## Merge informe Magia

- Cap: `<ruta>/analisis_magia_cap{N}.md`
- Relato: `<ruta>/analisis_magia.md`

Reescribir solo `## Ley cero`, `## Primera ley`, `## Segunda ley`, `## Tercera ley` de las leyes del foco; actualizar filas en `## Resumen de notas`. Resto intacto. Si no existía: plantilla completa; leyes no evaluadas = `—` en resumen y sección mínima «No evaluado en esta pasada».

Tras evaluar: ejecutar skill `guarda-analisis` (clave `Magia — Cap {N}` o `Magia — Relato`).

## Tras grill confirmado

**Una** pregunta: «¿Seguir con PPR?». Solo con **sí**: skill `recursor-escritura-creativa`. No escribir `promesas.md`, `sinopsis.md`, `esquema.md` ni Roadmap.

Skills de pilar pueden disparar esta pregunta en modo autónomo. La orquestadora, una sola vez al final.

## Plantilla `sistema_magia.md`

```markdown
# Sistema de magia: [nombre del relato]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## Impresionante
[Imagen o efecto que arranca el sistema. Trabajar hacia atrás desde aquí.]

## Poderes
- **[Nombre]:** qué hace / quién lo usa / semilla

## Defectos
- **[Nombre]:** qué se trabaja (práctica, comprender, magia rota) / clímax = superarlo

## Limitaciones
- **[Nombre]:** qué no se arregla / se convive / clímax = otro

## Costes
- **[Nombre]:** precio (recurso, consecuencia, deseo que se tuerce) / cuánto se usa

## Espectro
- **Posición:** dura | blanda | híbrida
- **El lector debe entender:** …
- **Queda como maravilla:** …
- **Indicios:** contradicciones aparentes, lagunas de serie

## Conflictos que la magia puede cerrar
- **[Conflicto]:** se estableció qué pasaría / tramo del pago / qué no puede cerrar

## Profundidad
- **Se amplía:** …
- **Se insinúa (iceberg hueco):** …
- **No existe todavía:** …

## Notas de riesgo
- [deus ex machina, poder nuevo al 95%, rareza que resuelve trama, catálogo sin gancho…]
```

## Plantilla informe Magia

```markdown
# Magia — [Relato | Cap N]

**Alcance:** relato | capítulo N
**Última evaluación:** YYYY-MM-DD

## Resumen de notas

| Ley | Nota | Última evaluación |
|-----|------|-------------------|
| Ley cero | — o N/10 | YYYY-MM-DD o — |
| Primera | — o N/10 | YYYY-MM-DD o — |
| Segunda | — o N/10 | YYYY-MM-DD o — |
| Tercera | — o N/10 | YYYY-MM-DD o — |

## Ley cero

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Primera ley

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Segunda ley

**Evaluado:** YYYY-MM-DD | **Nota:** N/10

### Hallazgos
- ...

### Propuestas
- ...

## Tercera ley

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
- No hace `AskQuestion`, no escribe ficheros, no llama `guarda-analisis`, no pregunta PPR.

## No hacer (todas las skills de magia)

- Copiar texto literal del libro fuente privado.
- Volcar anécdotas del capítulo a chat, ficheros o informes.
- Escribir `promesas.md`, `sinopsis.md`, `esquema.md` o Roadmap.
- Asumir leyes sin `AskQuestion` (salvo delegado).
- Repartir capítulos (`sugerencia-capitulos`).
- Grillar arco de personaje (PPR). Una línea en notas si el defecto de magia coincide con el del personaje.
- Inventar citas o reglas no presentes en texto/plan.

## Relación con otras skills

| Skill | Uso |
|-------|-----|
| `iniciar-relato` | Primero si falta relato activo |
| `guarda-analisis` | Tras informe Magia local |
| `leyes-magia` | Orquestadora (`SKILL.md` en esta carpeta) si foco tiene 2–4 leyes |
| `recursor-escritura-creativa` | Tras grill, solo si el escritor confirma |
| `chapter-editor` | Mismo criterio de localizar cap |
