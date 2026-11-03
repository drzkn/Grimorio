---
name: pov-evaluar
description: >-
  Auditar POV en capítulo o relato (Sanderson, cap. El punto de vista): saltos
  de cabeza, ocultación, fiabilidad, combinaciones. Triggers "evalúa POV",
  "evalúa punto de vista", "salto de cabeza", "head hopping", "narrador no
  fiable", "revisa el POV". Requiere modelo en esquema.md o inferido del texto.
---

# POV — Evaluar

Teoría y checklist: [teoria.md](../teoria.md). Localizar cap: mismo criterio que `chapter-editor` (`capitulo_N.md`, `capN.md`, sección en `contenido.md`).

Respuesta al usuario en **español**.

## Entrada

1. `iniciar-relato` si falta relato activo.
2. `AskQuestion`: alcance `Relato entero` | `Capítulo` (+ N si capítulo).

## Fuentes

- Texto del alcance elegido.
- `<ruta>/esquema.md` sección `# Punto de vista` si existe.
- `contexto_global/tono_narrador.md` si existe.
- `promesas.md` solo como contexto (no puntuar PPR).

Si no hay sección `# Punto de vista`: inferir modelo del texto, decirlo en el informe y evaluar contra lo inferido; sugerir `pov-elegir` para fijar canon en `esquema.md`.

Sin cita del texto, no hay hallazgo. **No** modificar `esquema.md`.

## Criterios

Usar checklist en [teoria.md](../teoria.md) más:

- Coherencia persona / tiempo / marco con modelo declarado o inferido.
- **Salto de cabeza** dentro de una escena (limitado, cinematográfico).
- Pensamientos ajenos en limitado sin filtro del POV («parecía pensar…» vs omnisciencia encubierta).
- Ocultación tramposa en limitado (el POV sabe y no piensa nada creíble).
- Demasiados narradores en 1.ª persona; lector pierde hilo de quién habla.
- POV o interludio nuevo sin preparación previa en el libro.
- Credibilidad epistolar (memoria literal, formato documento).
- Omnisciente verdadero: expectativa de anticipación vs sorpresa imposible.
- Volcados de información sin voz (1.ª) o sin anclaje escénico (3.ª).

Nota /10. Hallazgos con cita breve. Propuestas concretas (corte de escena, epígrafe, interludio, cambio de frase).

Guardar informe (plantilla abajo). Ejecutar `guarda-analisis` (clave `POV — Cap {N}` o `POV — Relato`).

## Plantilla informe

Cap: `<ruta>/analisis_pov_cap{N}.md`. Relato: `<ruta>/analisis_pov.md`.

```markdown
# POV — [Relato | Cap N]

**Alcance:** relato | capítulo N
**Modelo de referencia:** [desde esquema.md o inferido]
**Evaluado:** YYYY-MM-DD
**Nota:** N/10

## Hallazgos
- [cita o referencia] — …

## Propuestas
- …

## Diagnóstico (si aplica)
- Modelo / ocultación / reparto / combinaciones: …
```

## No hacer

- Copiar texto literal del libro fuente.
- Reescribir `esquema.md` (usar `pov-elegir`).
- Evaluar promesa/progreso/recompensa como informe PPR (solo impacto de POV si aplica).
- Inventar citas.

## Relación

| Skill | Uso |
|-------|-----|
| `pov-elegir` | Fijar `# Punto de vista` en `esquema.md` |
| `ppr-trama` | Esquema de tramas; no evalúa POV |
| `chapter-editor` | Edición general; puede mencionar POV |
| `guarda-analisis` | Tras informe local |
