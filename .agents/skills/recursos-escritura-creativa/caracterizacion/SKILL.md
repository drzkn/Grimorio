---
name: caracterizacion
description: >-
  Orquestadora caracterización (Sanderson, cap. Caracterización): diálogo,
  descripción, acción e introspección. Delega a dialogo/, descripcion/, accion/,
  introspeccion/. Un foco → skill de pilar. Triggers "caracterización", "voz del
  autor", "las cuatro escrituras", grill/evaluar caracterización.
---

# Caracterización — Orquestadora

Coordina las cuatro escrituras. Reglas: [comun.md](comun.md). Marco: [teoria.md](teoria.md).

| Pilar | Skill | Ruta |
|-------|--------|------|
| dialogo | `caracterizacion-dialogo` | [dialogo/SKILL.md](dialogo/SKILL.md) |
| descripcion | `caracterizacion-descripcion` | [descripcion/SKILL.md](descripcion/SKILL.md) |
| accion | `caracterizacion-accion` | [accion/SKILL.md](accion/SKILL.md) |
| introspeccion | `caracterizacion-introspeccion` | [introspeccion/SKILL.md](introspeccion/SKILL.md) |

## Cuándo usar

- Dos a cuatro pilares tras `AskQuestion` en `comun.md`.
- Petición genérica («caracterización», «voz», «mejorar diálogos»).
- Más de un pilar marcado al invocar un skill de pilar.

**No** para quién es el personaje → `personaje`. **No** para PPR. **No** para atlas → `mundo-entrega`.

## Cuándo NO

Un solo pilar → skill de pilar autónoma y parar.

## Flujo orquestador

1. `iniciar-relato` si falta.
2. `comun.md` entrada.
3. `|foco|=1` → delegar pilar; fin.
4. Dependencias `comun.md` (personajes / arco visible).
5. Leer marco + pilares en **modo delegado** + `teoria.md` cada uno. Semilla: `caracterizacion.md`, `personajes.md`, `promesas.md`.

### Grill (2–4)

1. Semilla.
2. Cerrado/abierto por pilar.
3. Árbol **dialogo → descripcion → accion → introspeccion**.
4. Rondas, confirmación.
5. Un `caracterizacion.md`.
6. Pregunta evaluar cap opcional (`comun.md`).

### Evaluar (2–4)

1. Fuentes.
2. Criterios por pilar delegado.
3. Un informe merge.
4. `guarda-analisis`.

## Modo delegado

Solo rama grill o evaluar del pilar. Sin `AskQuestion`, sin ficheros.

## No hacer

- Orquestar con un solo pilar.
- Duplicar `comun.md`.
- Listado § No hacer de `comun.md`.

## Relación

| Skill | Rol |
|-------|-----|
| Pilares `caracterizacion-*` | Autónomos o delegados |
| `personaje` | Lee `personajes.md` |
| `recursor-escritura-creativa` | Arco; no invocar desde aquí |
| `guarda-analisis` | Tras informe |
| `mundo-entrega` | Pirámide / sala blanca atlas |
| `chapter-editor` | Prosa; no sustituye esta pasada |