---
name: promesa-progreso-recompensa
description: >-
  Orquestadora PPR (Sanderson): varios pilares o petición genérica. Delega a
  ppr-promesa, ppr-progreso, ppr-recompensa. Un solo foco → skill de pilar
  autónoma. Triggers "PPR", "promesa-progreso-recompensa", "promesa progreso
  recompensa", grill/evaluar varios pilares.
---

# PPR — Orquestadora

Coordina promesa, progreso y recompensa. Reglas compartidas: [ppr-comun.md](../ppr-comun.md). Marco: [teoria.md](teoria.md).

Skills de pilar:

| Pilar | Skill |
|-------|--------|
| promesa | `ppr-promesa` |
| progreso | `ppr-progreso` |
| recompensa | `ppr-recompensa` |

## Cuándo usar esta skill

- Usuario pide **dos o tres** pilares (tras `AskQuestion` en `ppr-comun.md`).
- Petición genérica («trabaja PPR», «grill promesa progreso recompensa») sin skill de pilar concreta.
- Usuario invocó una skill de pilar y marcó **más de un** pilar en la pregunta de entrada.

## Cuándo NO (delegar a pilar)

Tras `AskQuestion`, si `foco` tiene **un solo** pilar: ejecutar la skill de pilar correspondiente **en modo autónomo** (flujo completo) y **parar**. No duplicar trabajo desde aquí.

## Flujo orquestador

1. `iniciar-relato` si falta relato activo.
2. Entrada: `ppr-comun.md` (pilares + alcance + camino grill/evaluar).
3. Si `|foco| = 1` → delegar a skill de pilar autónoma; fin.
4. Comprobar dependencias (`ppr-comun.md`) si `promesa` ∉ `foco`.
5. Leer `teoria.md` (marco) y, por cada pilar en `foco`, la skill de pilar en **modo delegado** (rama grill o criterios evaluar + `teoria.md` del pilar).

### Grill (2–3 pilares)

1. Semilla (`ppr-comun.md`).
2. Marcar cerrado/abierto por hilo y por pilar del foco.
3. **Árbol unificado:** ramas de cada skill de pilar en orden **promesa → progreso → recompensa**.
4. Rondas, riesgos, tope, confirmación (`ppr-comun.md`).
5. **Una** escritura `promesas.md` (merge de todos los pilares del foco).
6. **Una** pregunta volcado sinopsis si aplica (`ppr-comun.md`).

### Evaluar (2–3 pilares)

1. Fuentes (`ppr-comun.md`).
2. Aplicar criterios de cada skill de pilar en `foco` (modo delegado).
3. **Un** informe con merge de secciones evaluadas (`ppr-comun.md`).
4. **Un** `guarda-analisis`.

## Modo delegado (referencia)

Al leer `ppr-promesa` / `ppr-progreso` / `ppr-recompensa` desde aquí: solo secciones «Rama del grill» y «Evaluar» + su `teoria.md`. Sin `AskQuestion`, sin persistencia, sin Notion.

## No hacer

- Ejecutar orquestación cuando solo hay un pilar (usar skill de pilar).
- Duplicar plantillas o merge (están en `ppr-comun.md`).
- Lo listado en `ppr-comun.md` § No hacer.

## Relación

| Skill | Rol |
|-------|-----|
| `ppr-promesa` / `ppr-progreso` / `ppr-recompensa` | Un pilar; autónomas o delegadas |
| `sinopsis` | Volcado `## Promesas` si el escritor confirma |
| `guarda-analisis` | Tras informe PPR |
| `sugerencia-capitulos` | No invocar desde PPR |
