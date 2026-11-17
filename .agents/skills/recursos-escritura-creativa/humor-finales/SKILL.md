---
name: humor-finales
description: >-
  Orquestadora humor y finales (Sanderson, cap. Humor, finales y revisiones):
  humor, finales, revisiones. Delega a humor/, finales/, revisiones/. Un foco →
  skill de pilar. Triggers "humor", "finales", "sanderlancha", "revisiones",
  "guía de revisión", grill/evaluar humor o cierre.
---

# Humor y finales — Orquestadora

Coordina humor, finales y revisiones. Reglas: [comun.md](comun.md). Marco: [teoria.md](teoria.md).

| Pilar | Skill | Ruta |
|-------|--------|------|
| humor | `humor` | [humor/SKILL.md](humor/SKILL.md) |
| finales | `finales` | [finales/SKILL.md](finales/SKILL.md) |
| revisiones | `revisiones` | [revisiones/SKILL.md](revisiones/SKILL.md) |

## Cuándo usar

- Usuario pide **dos o tres** pilares (tras `AskQuestion` en `comun.md`).
- Petición genérica («trabaja el final», «humor y clímax») sin skill de pilar concreta.
- Usuario invocó un pilar y marcó **más de un** pilar en la entrada.

**No** para tipos de pago PPR solos → `ppr-recompensa`. **No** para tono y promesa temprana → `ppr-promesa`. **No** para diálogo genérico → `caracterizacion-dialogo`.

## Cuándo NO (delegar a pilar)

Tras `AskQuestion`, si `foco` tiene **un solo** pilar: ejecutar la skill de pilar **en modo autónomo** y **parar**.

## Flujo orquestador

1. `iniciar-relato` si falta relato activo.
2. Entrada: `comun.md` (pilares + alcance + camino grill/evaluar).
3. Si `|foco| = 1` → delegar a skill de pilar autónoma; fin.
4. Dependencias (`comun.md`): `finales` beneficia de `promesas.md` o texto con arcos visibles.
5. Leer `teoria.md` y, por cada pilar en `foco`, el `SKILL.md` del pilar en **modo delegado** + su `teoria.md`. Semilla: `humor-finales.md`, `revision.md`, `promesas.md`, `sinopsis.md`.

### Grill (2–3)

1. Semilla (`comun.md`).
2. Cerrado/abierto por pilar.
3. **Árbol unificado:** `humor` → `finales` → `revisiones`.
4. Rondas, riesgos, tope, confirmación (`comun.md`).
5. **Humor y/o finales:** un `humor-finales.md` (merge de esos pilares).
6. **Revisiones:** un `revision.md` si el foco incluye `revisiones`.
7. Pregunta PPR opcional si cambió el cierre (`comun.md`).

### Evaluar (2–3)

1. Fuentes (`comun.md`).
2. Criterios por pilar (modo delegado).
3. Informe merge (`comun.md`).
4. `guarda-analisis` según pilar.

## Modo delegado

Al leer skills de pilar desde aquí: solo «Rama del grill» y «Evaluar» + `teoria.md`. Sin `AskQuestion`, sin persistencia, sin Notion.

## No hacer

- Orquestar con un solo pilar.
- Duplicar plantillas (`comun.md`).
- Lo listado en `comun.md` § No hacer.

## Relación

| Skill | Rol |
|-------|-----|
| Pilares `humor`, `finales`, `revisiones` | Autónomos o delegados |
| `recursor-escritura-creativa` | Promesas y recompensas; lee, no reescribe desde aquí |
| `ppr-recompensa` | Tipos de pago; clímax detallado en `finales/` |
| `caracterizacion-dialogo` | Voz y acotaciones; taxonomía del chiste en `humor/` |
| `personaje` | Escalas, muerte de personaje, partir POV |
| `guarda-analisis` | Tras informes locales |
| `chapter-editor` | Prosa; pasada 5.0 en `revisiones/` |