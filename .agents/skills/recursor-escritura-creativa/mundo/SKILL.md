---
name: mundo
description: >-
  Orquestadora mundo (Sanderson, cap. Cómo crear un mundo): varios pilares o
  petición genérica. Delega a entrega/, construccion/, consistencia/. Un solo
  foco → skill de pilar. Triggers "mundo", "ambientación", "construcción del
  mundo", "worldbuilding", grill/evaluar varios pilares de mundo.
---

# Mundo — Orquestadora

Coordina entrega, construcción y consistencia. Reglas: [comun.md](comun.md). Marco: [teoria.md](teoria.md).

Skills de pilar (misma carpeta):

| Pilar | Skill | Ruta |
|-------|--------|------|
| entrega | `mundo-entrega` | [entrega/SKILL.md](entrega/SKILL.md) |
| construccion | `mundo-construccion` | [construccion/SKILL.md](construccion/SKILL.md) |
| consistencia | `mundo-consistencia` | [consistencia/SKILL.md](consistencia/SKILL.md) |

## Cuándo usar esta skill

- Usuario pide **dos o tres** pilares de mundo (tras `AskQuestion` en `comun.md`).
- Petición genérica («trabaja el mundo», «ambientación», «worldbuilding») sin skill de pilar concreta.
- Usuario invocó un pilar y marcó **más de un** pilar en la pregunta de entrada.

**No** usar para enciclopedia de autor (`esquema.md` `# Ambientación`) → `ppr-trama`. **No** usar para leyes de magia → familia `leyes-magia`.

## Cuándo NO (delegar a pilar)

Tras `AskQuestion`, si `foco` tiene **un solo** pilar: ejecutar la skill de pilar correspondiente **en modo autónomo** y **parar**.

## Flujo orquestador

1. `iniciar-relato` si falta relato activo.
2. Entrada: `comun.md` (pilares + alcance + camino grill/evaluar).
3. Si `|foco| = 1` → delegar a skill de pilar autónoma; fin.
4. Comprobar dependencias (`comun.md`) si `construccion` ∉ `foco`.
5. Leer `teoria.md` (marco) y, por cada pilar en `foco`, el `SKILL.md` del pilar en **modo delegado** + su `teoria.md`. Si existe `esquema.md` o `contexto.md`, usarlos como semilla (contexto = solo lectura).

### Grill (2–3 pilares)

1. Semilla (`comun.md`).
2. Marcar cerrado/abierto por elemento y por pilar del foco.
3. **Árbol unificado:** ramas de `construccion/`, `consistencia/`, `entrega/` en orden **construccion → consistencia → entrega**.
4. Rondas, riesgos, tope, confirmación (`comun.md`).
5. **Una** escritura `mundo.md` (merge de todos los pilares del foco).
6. **Una** pregunta volcado esquema si aplica (`comun.md`).

### Evaluar (2–3 pilares)

1. Fuentes (`comun.md`).
2. Criterios de cada pilar en `foco` (modo delegado).
3. **Un** informe con merge (`comun.md`).
4. **Un** `guarda-analisis`.

## Modo delegado (referencia)

Al leer `entrega/SKILL.md`, `construccion/SKILL.md` o `consistencia/SKILL.md` desde aquí: solo «Rama del grill» y «Evaluar» + `teoria.md` del pilar. Sin `AskQuestion`, sin persistencia, sin Notion.

## No hacer

- Orquestar cuando solo hay un pilar (usar skill de pilar).
- Duplicar plantillas o merge (están en `comun.md`).
- Lo listado en `comun.md` § No hacer.

## Relación

| Skill | Rol |
|-------|-----|
| `mundo-entrega` / `mundo-construccion` / `mundo-consistencia` | Pilares; autónomas o delegadas |
| `ppr-trama` | Enciclopedia `# Ambientación`; no entra en foco mundo |
| `guarda-analisis` | Tras informe mundo |
| `sugerencia-capitulos` | No invocar desde mundo |
| `build-context` | No invocar; `contexto.md` semilla |
| `leyes-magia` | Sistemas de magia; no duplicar |
