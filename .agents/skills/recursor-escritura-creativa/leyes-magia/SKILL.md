---
name: leyes-magia
description: >-
  Orquestadora de las leyes de Sanderson (cap. Las leyes de la magia): varios
  pilares o petición genérica de pulir el sistema. Delega a cero/, primera/,
  segunda/, tercera/. Un solo foco → skill de pilar. Triggers "sistema de
  magia", "leyes de Sanderson", "grill de magia", "pulir la magia",
  "leyes-magia".
---

# Leyes de la magia — Orquestadora

Pack del curso: carpeta padre [recursor-escritura-creativa/](../SKILL.md). PPR no entra en este foco.

Coordina las cuatro leyes. Reglas: [comun.md](comun.md). Marco: [teoria.md](teoria.md).

Skills de pilar (misma carpeta):

| Ley | Skill | Ruta |
|-----|--------|------|
| cero | `magia-ley-cero` | [cero/SKILL.md](cero/SKILL.md) |
| primera | `magia-primera-ley` | [primera/SKILL.md](primera/SKILL.md) |
| segunda | `magia-segunda-ley` | [segunda/SKILL.md](segunda/SKILL.md) |
| tercera | `magia-tercera-ley` | [tercera/SKILL.md](tercera/SKILL.md) |

## Cuándo usar esta skill

- Usuario pide **dos o más** leyes (tras `AskQuestion` en `comun.md`).
- Petición genérica («pulir la magia», «grill de magia», «sistema de magia») sin skill de pilar concreta.
- Usuario invocó un pilar y marcó **más de una** ley en la pregunta de entrada.

## Cuándo NO (delegar a pilar)

Tras `AskQuestion`, si `foco` tiene **una sola** ley: ejecutar la skill de pilar correspondiente **en modo autónomo** y **parar**.

## Flujo orquestador

1. `iniciar-relato` si falta relato activo.
2. Entrada: `comun.md` (leyes + alcance + camino grill/evaluar). Petición genérica: proponer las cuatro, sin asumirlas si no marcan.
3. Si `|foco| = 1` → delegar a skill de pilar autónoma; fin.
4. Comprobar dependencias (`comun.md`) si `cero` ∉ `foco`.
5. Leer `teoria.md` (marco) y, por cada ley en `foco`, el `SKILL.md` del pilar en **modo delegado** + su `teoria.md`.

### Grill (2–4 leyes)

1. Semilla (`comun.md`).
2. Marcar cerrado/abierto por decisión y por ley del foco.
3. **Árbol unificado:** ramas de `cero/`, `segunda/`, `primera/`, `tercera/` en orden **cero → segunda → primera → tercera**. Solo las leyes en `foco`.
4. Rondas, riesgos, tope, confirmación (`comun.md`).
5. **Una** escritura `sistema_magia.md` (merge de todas las leyes del foco).
6. **Una** pregunta PPR si aplica (`comun.md`).

### Evaluar (2–4 leyes)

1. Fuentes (`comun.md`).
2. Criterios de cada ley en `foco` (modo delegado).
3. **Un** informe con merge (`comun.md`).
4. **Un** `guarda-analisis`.

## Modo delegado (referencia)

Al leer `cero/SKILL.md`, `primera/SKILL.md`, `segunda/SKILL.md` o `tercera/SKILL.md` desde aquí: solo «Rama del grill» y «Evaluar» + `teoria.md` del pilar. Sin `AskQuestion`, sin persistencia, sin Notion.

## No hacer

- Orquestar cuando solo hay una ley (usar skill de pilar).
- Duplicar plantillas o merge (están en `comun.md`).
- Lo listado en `comun.md` § No hacer.

## Relación

| Skill | Rol |
|-------|-----|
| `magia-ley-cero` / `magia-primera-ley` / `magia-segunda-ley` / `magia-tercera-ley` | Pilares; autónomas o delegadas |
| `guarda-analisis` | Tras informe Magia |
| `recursor-escritura-creativa` | Tras grill, solo si el escritor confirma |
| `sugerencia-capitulos` | No invocar desde aquí |
