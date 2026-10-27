---
name: promesa-progreso-recompensa
description: >-
  Promesa, progreso y recompensa (Sanderson, cap. La trama): grill estilo
  grill-me para definirlos en el relato, evaluación global o por capítulo,
  fichero promesas.md y opcionalmente sinopsis. Triggers: "promesas",
  "progreso", "recompensas", "promesa-progreso-recompensa", "grill de
  promesas", "evalúa promesas/progreso/recompensa", "PPR", cap o relato.
---

# Promesa, progreso, recompensa

Tres pilares de enganche narrativo. Teoría en [teoria.md](teoria.md) — leer al grillar o evaluar.

Respuesta al usuario en **español**.

## Capas (no mezclar)

| Path | Qué es |
|------|--------|
| `<ruta>/promesas.md` | Canon local de promesas, progreso planificado y recompensas por hilo |
| Notion `Roadmap` + `<ruta>/sinopsis.md` | Plan de obra. Sección `## Promesas` solo con confirmación explícita del escritor |
| `<ruta>/analisis_ppr.md` | Evaluación PPR del relato entero |
| `<ruta>/analisis_ppr_cap{N}.md` | Evaluación PPR del capítulo N |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Entrada: confirmar pilares y alcance

**Siempre** antes de grill o evaluar, aunque el mensaje ya nombre pilares o alcance.

`AskQuestion` en un solo formulario:

1. **Pilares** (`allow_multiple: true`): opciones `Promesa`, `Progreso`, `Recompensa`. Enunciado: «¿Qué pilares quieres trabajar?». Si el mensaje sugería algunos: «Has mencionado […]; confirma o marca otros».
2. **Alcance** (solo si no quedó claro en el mensaje): `Relato entero` | `Capítulo` (+ pedir N si eligen capítulo).

Sin ningún pilar marcado: repetir la pregunta **una vez**. No asumir los tres.

Guardar en sesión:

- `foco` ⊆ {`promesa`, `progreso`, `recompensa`}, no vacío.
- `alcance` = `relato` | `cap {N}`.

### Pilares fuera del foco

Leer de `promesas.md`, `sinopsis.md` o texto. **No** preguntar ni puntuar.

### Dependencias

Progreso y recompensa cuelgan de promesas definidas. Si `promesa` ∉ `foco` y no hay promesas en `promesas.md` ni deducibles de sinopsis/texto:

- Avisar.
- Ofrecer: añadir `promesa` al foco, o una ronda mínima solo para fijar las promesas que esos pilares necesitan.

En grill con varios pilares: un árbol; frontera respeta orden **promesa → progreso → recompensa** (no progreso/recompensa de un hilo aún abierto en el grill).

## Caminos

| Intención del usuario | Camino |
|----------------------|--------|
| definir, grill, afilar, planificar promesas/PPR | **Grill** |
| evaluar, auditar, nota, revisar en texto escrito | **Evaluar** |

Si no queda claro grill vs evaluar: una pregunta en el mismo `AskQuestion` o justo después de pilares/alcance.

---

## Camino Grill (estilo grill-me; formato como `sinopsis`)

1. **Relato activo** (`iniciar-relato`).
2. Confirmar pilares y alcance (arriba).
3. **Semilla** (orden):
   - `<ruta>/promesas.md` si existe.
   - `sinopsis.md` tras volcar `Roadmap` según skill `sinopsis` (solo traer; no grillar sinopsis).
   - `contexto_global/`, caps del relato.
   - Mensaje del escritor, si no hay nada local.
   - Sin semilla: una pregunta («pega premisa o qué prometes al lector») y parar.
4. Leer [teoria.md](teoria.md). Marcar por hilo y por pilar del foco: **cerrado** vs **abierto** (hueco, contradicción, choque con texto escrito).
5. **Árbol** (podado al foco):
   - `promesa`: tono, arcos (o emblemático), paraguas / nuclear, anidamiento, minipromesas.
   - `progreso`: por promesa fijada — hitos, tramos, pasos atrás, ganchos de cap, riesgo desvío.
   - `recompensa`: por promesa fijada — qué se entrega, tipo (directa / expansión / sustitución), preparación, dónde se paga, deriva del progreso.
6. **Frontera** = decisiones abiertas cuyas previas están cerradas. Una ronda = frontera entera, numerada, recomendación `➡️`; «sí» acepta la recomendación.

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <lectura desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

7. Señalar riesgos con teoría (minipromesa accidental, subtrama-desvío, sustitución sin preparar).
8. Recalcular frontera tras respuestas. **Tope**: huecos que cambian compromisos con el lector. Prosa ya fijada, reparto de caps: fuera (`sugerencia-capitulos`).
9. Frontera vacía → resumir lo acordado (solo pilares del foco). Esperar confirmación de entendimiento común.
10. Escribir `<ruta>/promesas.md`: **solo** secciones/columnas de los pilares del foco; el resto intacto. Crear fichero con plantilla completa si no existía.
11. Si el foco incluía `promesa` o `recompensa` **y** hubo cambios en hilos («se abre en» / «se paga en»): preguntar «¿Vuelco las promesas a la sección Promesas de la sinopsis (Roadmap)?». Solo con **sí**: actualizar `## Promesas` en `Roadmap` + `sinopsis.md` (skill `sinopsis`, mismo turno, formato `- **[Hilo]:** se abre en … / se paga en … / estado`). Grill solo de `progreso` → no preguntar.
12. Informar ruta de `promesas.md`. 2–4 líneas; no volcar el fichero entero al chat.

---

## Camino Evaluar

1. Relato activo + confirmar pilares y alcance.
2. Leer [teoria.md](teoria.md) y checklist.
3. **Fuentes**:
   - Alcance cap: texto del cap (mismo criterio que `chapter-editor`: `capitulo_N.md`, `capN.md`, o sección en `contenido.md`).
   - Alcance relato: caps disponibles + merge `contexto_global/` si existe.
   - `promesas.md`, `sinopsis.md` si existen.
   - `contexto_global/capitulos/<N>.md` cuando aplique.
4. Evaluar **solo** pilares del foco. Sin cita del texto o del plan, no hay hallazgo.
5. Si hay `promesas.md`, contrastar plan vs texto; no modificar `promesas.md` sin preguntar.

### Criterios por pilar (cap N)

| Pilar | Qué mirar |
|-------|-----------|
| Promesa | Promesas abiertas/avanzadas/pagadas en el cap; tono; arco; minipromesas nuevas |
| Progreso | Escenas que avanzan objetivo vs escenas muertas; pasos atrás; ganchos (legítimo vs pizza); desvío percibido |
| Recompensa | Pagos parciales; si el cap acerca el pago prometido; coherencia con tipo previsto |

### Criterios por pilar (relato)

| Pilar | Qué mirar |
|-------|-----------|
| Promesa | Mapa apertura → cierre; huérfanas; tono inicial vs cuerpo; presentación larga |
| Progreso | Hilos estancados; subtramas-desvío; anidamiento; page-turner global |
| Recompensa | Tipo de cada pago; derivación del progreso; promesas rotas |

Propuestas concretas; ante desvío tipo Shadesmar, **preferir cambiar promesa** antes que reescribir todo el progreso (Sanderson).

6. **Guardar informe** (merge por secciones):
   - Cap: `<ruta>/analisis_ppr_cap{N}.md`
   - Relato: `<ruta>/analisis_ppr.md`
   - Si el fichero existe: reescribir solo `## Promesa`, `## Progreso`, `## Recompensa` de los pilares del foco; cabecera y otras secciones intactas.
   - Si no existe: plantilla completa; pilares no evaluados en cuerpo = «—» o sección mínima «No evaluado en esta pasada».
7. Ejecutar skill `guarda-analisis` (toggle PPR).
8. Chat: notas /10 de los pilares evaluados + 2–4 líneas de veredicto.

---

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

---

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
- [cita o referencia] — ...

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

Al evaluar un subconjunto de pilares: actualizar filas de «Resumen de notas» y secciones correspondientes; dejar el resto como estaba en el fichero previo.

---

## No hacer

- Copiar texto literal del libro fuente privado.
- Escribir en `Roadmap` / `sinopsis.md` sin confirmación explícita.
- Asumir los tres pilares sin `AskQuestion`.
- Repartir capítulos (`sugerencia-capitulos`).
- Modificar `promesas.md` en evaluar sin permiso del escritor.
- Inventar citas o promesas no presentes en texto/plan.

## Relación con otras skills

| Skill | Qué hacer |
|-------|-----------|
| `iniciar-relato` | Primero si falta relato activo |
| `sinopsis` | Traer Roadmap; volcar `## Promesas` solo si el escritor confirma tras grill |
| `guarda-analisis` | Tras guardar informe PPR local |
| `chapter-editor` | Mismo criterio de localizar cap; puede contrastar desvíos con `promesas.md` / sinopsis |
| `sugerencia-capitulos` | No invocar desde esta skill |
