---
name: pov-elegir
description: >-
  Elegir y afilar modelo narrativo (Sanderson, cap. El punto de vista): grill
  que escribe la sección # Punto de vista en esquema.md. Triggers "POV",
  "punto de vista", "narrador", "qué persona", "elegir POV", "primera o
  tercera", "omnisciente limitado", "flashback". No sustituye PPR ni sinopsis.
---

# POV — Elegir (grill)

Teoría: [teoria.md](../teoria.md). Rondas: [comun.md](../../comun.md) (formato grill). **No** entra en pilares PPR.

Respuesta al usuario en **español**.

## Entrada

1. `iniciar-relato` si falta relato activo.
2. Alcance = **relato entero** (no capítulo suelto).

## Semilla (grill)

Orden:

1. `<ruta>/esquema.md` (sección `# Punto de vista` si existe).
2. `<ruta>/promesas.md`, `sinopsis.md` (Roadmap vía `sinopsis` si hace falta).
3. `contexto_global/tono_narrador.md`, `contexto_global/`, caps escritos.
4. Mensaje del escritor.

Sin nada usable: una pregunta («¿1.ª o 3.ª? ¿Un narrador o reparto?») y parar.

## Camino Grill

Leer [teoria.md](../teoria.md). Marcar cerrado/abierto. **Frontera** en este orden:

1. **Persona y modelo principal:** 2.ª persona (solo si consciente) | epistolar | flashback | cinematográfico | narrador presente | omnisciente verdadero | omnisciente limitado.
2. **Personajes POV:** quién(es); reparto; avisar si >2–3 en 1.ª persona.
3. **Tiempo verbal** (presente / pasado) y **historia marco** (sí/no; qué contraste aporta).
4. **Información oculta:** secretos al lector; técnica por modelo (epistolar, voz 1.ª, trampa justificada en limitado, anticipación en verdadero).
5. **Fiabilidad:** narrador fiable | no fiable (y en qué modelo encaja).
6. **Combinaciones:** epígrafes epistolares, documentos sueltos, interludios en otro modelo; POV tardíos a preparar desde el inicio.

Rondas = formato `comun.md`. Frontera vacía → resumen → confirmación.

**Persistencia:** merge **solo** la sección `# Punto de vista` en `<ruta>/esquema.md`. Si no existe `esquema.md`, crear fichero con cabecera mínima (nombre relato, fechas como en plantilla `ppr-trama`) y secciones `# Personajes`, `# Ambientación`, `# Trama` vacías o «pendiente» si el escritor no tiene esquema aún. **No** reescribir otras secciones de `esquema.md`.

Actualizar fechas en cabecera de `esquema.md`. **No** escribir `sinopsis.md` ni `promesas.md`.

Preguntar: «¿Siguiente paso?» — **auditar texto** (`pov-evaluar`) | **esquema de tramas** (`ppr-trama`) | **parar**.

## Plantilla `# Punto de vista` (dentro de `esquema.md`)

```markdown
# Punto de vista

**Modelo principal:** …
**Persona / tiempo:** …
**Historia marco:** …
**Personajes POV:** …
**Fiabilidad:** …
**Ocultación:** [secreto → técnica]
**Combinaciones:** …
**Riesgos:** …
```

## No hacer

- Copiar texto literal del libro fuente.
- Escribir `sinopsis.md`, `promesas.md`, `Roadmap` desde esta skill.
- Reescribir `# Personajes`, `# Ambientación`, `# Trama` de `esquema.md` (skill `ppr-trama`).
- Entrar en pregunta de pilares PPR.

## Relación

| Skill | Uso |
|-------|-----|
| `ppr-trama` | Resto de `esquema.md`; no tocar `# Punto de vista` |
| `pov-evaluar` | Tras decidir modelo, auditar caps o relato |
| `recursor-escritura-creativa` | PPR independiente del POV |
| `sinopsis` | No escribir desde aquí |
