---
name: personaje
description: >-
  Orquestadora personaje (Sanderson, cap. Cómo crear un personaje): varios
  pilares o petición genérica. Delega a escalas/, motivacion/, limites/. Un solo
  foco → skill de pilar. Triggers "personajes", "construcción de personaje",
  grill/evaluar varios pilares de personaje.
---

# Personaje — Orquestadora

Coordina escalas, motivación y límites. Reglas: [comun.md](comun.md). Marco: [teoria.md](teoria.md).

Skills de pilar (misma carpeta):

| Pilar | Skill | Ruta |
|-------|--------|------|
| escalas | `personaje-escalas` | [escalas/SKILL.md](escalas/SKILL.md) |
| motivacion | `personaje-motivacion` | [motivacion/SKILL.md](motivacion/SKILL.md) |
| limites | `personaje-limites` | [limites/SKILL.md](limites/SKILL.md) |

## Cuándo usar esta skill

- Usuario pide **dos o tres** pilares de personaje (tras `AskQuestion` en `comun.md`).
- Petición genérica («trabaja los personajes», «escalas y motivo») sin skill de pilar concreta.
- Usuario invocó un pilar y marcó **más de un** pilar en la pregunta de entrada.

**No** usar para esquema de trama ni fichas largas de autor (`ppr-trama`). **No** usar para promesa/arco PPR → `recursor-escritura-creativa`. **No** usar para leyes de magia → `leyes-magia`.

## Cuándo NO (delegar a pilar)

Tras `AskQuestion`, si `foco` tiene **un solo** pilar: ejecutar la skill de pilar correspondiente **en modo autónomo** y **parar**.

## Flujo orquestador

1. `iniciar-relato` si falta relato activo.
2. Entrada: `comun.md` (pilares + alcance + camino grill/evaluar).
3. Si `|foco| = 1` → delegar a skill de pilar autónoma; fin.
4. Comprobar dependencias (`comun.md`) si `motivacion` ∉ `foco` y hace falta motivo para `limites`.
5. Leer `teoria.md` (marco) y, por cada pilar en `foco`, el `SKILL.md` del pilar en **modo delegado** + su `teoria.md`. Si existe `esquema.md` `# Personajes` o `personajes.md`, usarlos como semilla.

### Grill (2–3 pilares)

1. Semilla (`comun.md`).
2. Marcar cerrado/abierto por personaje y por pilar del foco.
3. **Árbol unificado:** ramas de `escalas/`, `motivacion/`, `limites/` en orden **escalas → motivacion → limites**.
4. Rondas, riesgos, tope, confirmación (`comun.md`).
5. **Una** escritura `personajes.md` (merge de todos los pilares del foco).
6. Pregunta volcado esquema si aplica (`comun.md`).
7. Pregunta PPR si aplica (`comun.md`).

### Evaluar (2–3 pilares)

1. Fuentes (`comun.md`).
2. Criterios de cada pilar en `foco` (modo delegado).
3. **Un** informe con merge (`comun.md`).
4. **Un** `guarda-analisis`.

## Modo delegado (referencia)

Al leer `escalas/SKILL.md`, `motivacion/SKILL.md` o `limites/SKILL.md` desde aquí: solo «Rama del grill» y «Evaluar» + `teoria.md` del pilar. Sin `AskQuestion`, sin persistencia, sin Notion.

## No hacer

- Orquestar cuando solo hay un pilar (usar skill de pilar).
- Duplicar plantillas o merge (están en `comun.md`).
- Lo listado en `comun.md` § No hacer.

## Relación

| Skill | Rol |
|-------|-----|
| `personaje-escalas` / `personaje-motivacion` / `personaje-limites` | Pilares; autónomas o delegadas |
| `ppr-trama` | Fichas `# Personajes` en `esquema.md` |
| `recursor-escritura-creativa` | Tras grill, si el escritor confirma |
| `guarda-analisis` | Tras informe Personajes |
| `sugerencia-capitulos` | No invocar desde personaje |
| `mundo` | Ambientación; no duplicar |
| `leyes-magia` | Magia; restricciones de poder allí |
| `caracterizacion` | Cómo se ve en prosa (`caracterizacion.md`); no quién es |