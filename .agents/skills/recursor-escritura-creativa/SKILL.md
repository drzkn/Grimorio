---
name: recursor-escritura-creativa
description: >-
  Orquestadora PPR (Sanderson, caps. La trama y Cómo crear una trama): varios
  pilares o petición genérica. Delega a promesa/, progreso/, recompensa/. Un
  solo foco → skill de pilar. Esquema/arquetipos → ppr-trama. Triggers "PPR",
  "recursor-escritura-creativa", "promesa-progreso-recompensa", grill/evaluar
  varios pilares.
---

# PPR — Orquestadora

Coordina promesa, progreso y recompensa. Reglas: [comun.md](comun.md). Marco: [teoria.md](teoria.md). Esquema y arquetipos: [construir-trama.md](construir-trama.md).

Skills de pilar (misma carpeta):

| Pilar | Skill | Ruta |
|-------|--------|------|
| promesa | `ppr-promesa` | [promesa/SKILL.md](promesa/SKILL.md) |
| progreso | `ppr-progreso` | [progreso/SKILL.md](progreso/SKILL.md) |
| recompensa | `ppr-recompensa` | [recompensa/SKILL.md](recompensa/SKILL.md) |
| esquema / arquetipos | `ppr-trama` | [trama/SKILL.md](trama/SKILL.md) |
| POV (grill) | `pov-elegir` | [punto-de-vista/elegir/SKILL.md](punto-de-vista/elegir/SKILL.md) |
| POV (auditar) | `pov-evaluar` | [punto-de-vista/evaluar/SKILL.md](punto-de-vista/evaluar/SKILL.md) |

Teoría: [punto-de-vista/teoria.md](punto-de-vista/teoria.md). **No** entran en foco PPR.

## Cuándo usar esta skill

- Usuario pide **dos o tres** pilares PPR (tras `AskQuestion` en `comun.md`).
- Petición genérica («trabaja PPR») sin skill de pilar concreta.
- Usuario invocó un pilar y marcó **más de un** pilar en la pregunta de entrada.

**No** usar para esquema de trama → `ppr-trama`.

## Cuándo NO (delegar a pilar)

Tras `AskQuestion`, si `foco` tiene **un solo** pilar: ejecutar la skill de pilar correspondiente **en modo autónomo** y **parar**.

## Flujo orquestador

1. `iniciar-relato` si falta relato activo.
2. Entrada: `comun.md` (pilares + alcance + camino grill/evaluar).
3. Si `|foco| = 1` → delegar a skill de pilar autónoma; fin.
4. Comprobar dependencias (`comun.md`) si `promesa` ∉ `foco`.
5. Leer `teoria.md` (marco) y, por cada pilar en `foco`, el `SKILL.md` del pilar en **modo delegado** + su `teoria.md`. Si existe `esquema.md`, usarlo como contexto de arquetipos.

### Grill (2–3 pilares)

1. Semilla (`comun.md`).
2. Marcar cerrado/abierto por hilo y por pilar del foco.
3. **Árbol unificado:** ramas de `promesa/`, `progreso/`, `recompensa/` en orden **promesa → progreso → recompensa**.
4. Rondas, riesgos, tope, confirmación (`comun.md`).
5. **Una** escritura `promesas.md` (merge de todos los pilares del foco).
6. **Una** pregunta volcado sinopsis si aplica (`comun.md`).

### Evaluar (2–3 pilares)

1. Fuentes (`comun.md`).
2. Criterios de cada pilar en `foco` (modo delegado).
3. **Un** informe con merge (`comun.md`).
4. **Un** `guarda-analisis`.

## Modo delegado (referencia)

Al leer `promesa/SKILL.md`, `progreso/SKILL.md` o `recompensa/SKILL.md` desde aquí: solo «Rama del grill» y «Evaluar» + `teoria.md` del pilar. Sin `AskQuestion`, sin persistencia, sin Notion.

## No hacer

- Orquestar cuando solo hay un pilar (usar skill de pilar).
- Duplicar plantillas o merge (están en `comun.md`).
- Lo listado en `comun.md` § No hacer.

## Relación

| Skill | Rol |
|-------|-----|
| `ppr-promesa` / `ppr-progreso` / `ppr-recompensa` | Pilares; autónomas o delegadas |
| `ppr-trama` | Esquema `esquema.md` antes o en paralelo; no entra en foco PPR |
| `pov-elegir` / `pov-evaluar` | Cap. El punto de vista; fuera de PPR |
| `sinopsis` | Volcado `## Promesas` si el escritor confirma |
| `guarda-analisis` | Tras informe PPR |
| `sugerencia-capitulos` | No invocar desde PPR |
