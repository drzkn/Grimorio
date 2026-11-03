---
name: ppr-trama
description: >-
  Esquema y arquetipos de trama (Sanderson, cap. Cómo crear una trama): grill
  que escribe esquema.md, evaluar estructura del relato. Triggers "esquema de
  trama", "arquetipo", "construir la trama", "tres actos", "periplo del héroe",
  "evalúa la estructura". No sustituye PPR ni sinopsis.
---

# PPR — Trama (esquema y arquetipos)

Teoría: [construir-trama.md](../construir-trama.md). Reglas grill: [comun.md](../comun.md) (formato rondas). **No** entra en la pregunta de pilares PPR.

Respuesta al usuario en **español**.

## Entrada

1. `iniciar-relato` si falta relato activo.
2. `AskQuestion`: `Grill` (definir esquema) | `Evaluar` (auditar estructura en texto). Alcance = **relato entero** (no capítulo).

## Semilla (grill)

Orden:

1. `<ruta>/esquema.md` si existe.
2. `<ruta>/promesas.md`, `sinopsis.md` (Roadmap vía skill `sinopsis` si hace falta).
3. `contexto_global/`, caps escritos.
4. Mensaje del escritor.

Sin nada usable: una pregunta («¿premisa o tramas que ya tengas?») y parar.

## Camino Grill

Leer [construir-trama.md](../construir-trama.md). Marcar cerrado/abierto. **Frontera** en este orden:

1. **Forma de trabajo:** esquemático | descubrimiento | mixto. Si descubrimiento dominante: versión ligera (tramas + «Sí, pero / No, y» + giros previstos); omitir detalle de tres actos salvo que el escritor lo pida.
2. **Inventario de tramas** (3–5 en épica; mínimo novela: 1 arquetipo + 1 arco + 1 subtrama arquetípica). Arquetipo de cada una.
3. **Trama núcleo** y **columna reconocible** (obra coral).
4. **Por trama:** por qué gusta; elementos imprescindibles; objetivo final (planificar hacia atrás); lista de pasos (ideas, no escenas).
5. **Costuras** entre tramas (una resuelve hueco de otra).
6. **Estructura opcional:** hitos tres actos, punto medio, convergencia en clímax.
7. **Obras largas:** Jordan / secuencial / híbrido; hitos antes de separaciones.
8. **Giros previstos:** emoción + propósito; ampliar o recrudecer.

Rondas = formato `comun.md`. Frontera vacía → resumen → confirmación.

Escribir `<ruta>/esquema.md` (plantilla abajo). Actualizar fechas. **No** reescribir `# Punto de vista` si ya existe (dueña `pov-elegir`). **No** escribir `sinopsis.md` ni `promesas.md`.

Preguntar: «¿Siguiente paso?» — **PPR** de estas tramas (`recursor-escritura-creativa`) | **escaleta** (`sugerencia-capitulos`) | **parar**.

## Camino Evaluar

Fuentes: caps + `contexto_global/`, `esquema.md`, `promesas.md`, `sinopsis.md` si existen.

Criterios ([construir-trama.md](../construir-trama.md) checklist ampliado):

- Arquetipo por trama principal; núcleo vs tiempo del lector.
- Progreso medido en arquetipo real.
- Líneas sin cierre intermedio antes de larga ausencia.
- Giros sin propósito; promesas rotas al 75 % sin preparación.
- Convergencia en clímax; preparación reutilizada en giros tipo *Italian Job*.
- Mínimo de tramas según extensión; columna en coral.

Si «no funciona»: descomponer motivaciones, promesas, arquetipo/trayectoria, ritmo.

Guardar `<ruta>/analisis_trama.md` (plantilla abajo). Ejecutar `guarda-analisis` (clave `Trama — Relato`).

## Plantilla `esquema.md`

```markdown
# Esquema: [nombre del relato]

**Estado:** borrador | vigente
**Forma de trabajo:** esquema | descubrimiento | mixto
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

**Trama núcleo:** [nombre / arquetipo]
**Columna reconocible:** [si aplica]

# Personajes
## [Principal]
Presentación: …
Arcos: …
## Secundarios
### [Nombre]
…

# Ambientación
[Entradas breves o «ver contexto_global/…»]

# Punto de vista
**Modelo principal:** …
**Persona / tiempo:** …
**Historia marco:** …
**Personajes POV:** …
**Fiabilidad:** …
**Ocultación:** [secreto → técnica]
**Combinaciones:** …
**Riesgos:** …

# Trama
## [Trama 1 — arquetipo]
**Por qué gusta:** …
**Imprescindible:** …
**Objetivo final:** …
**Pasos:**
1. …
2. …
**Costuras:** [con otras tramas]
**Giros previstos:** …

## [Trama 2 — arquetipo]
…

# Estructura (opcional)
- Acto 1 → …
- Punto medio → …
- Punto más bajo → …
- Convergencia clímax → …

# Gestión líneas largas (opcional)
[Jordan / secuencial / híbrido; notas]
```

## Plantilla `analisis_trama.md`

```markdown
# Trama — [nombre del relato]

**Evaluado:** YYYY-MM-DD
**Nota:** N/10

## Hallazgos
- [cita o referencia] — …

## Propuestas
- …

## Diagnóstico (si aplica)
- Motivaciones / promesas / arquetipo / ritmo: …
```

## No hacer

- Copiar texto literal del libro.
- Escribir `sinopsis.md`, `promesas.md`, `Roadmap` desde esta skill.
- Repartir caps (solo ofrecer `sugerencia-capitulos`).
- Entrar en pregunta de pilares PPR (orquestadora aparte).
- Reescribir `# Punto de vista` en `esquema.md` (skill `pov-elegir`).

## Relación

| Skill | Uso |
|-------|-----|
| `recursor-escritura-creativa` | Tras esquema, grill/evaluar PPR por trama |
| `pov-elegir` | Sección `# Punto de vista` en `esquema.md` |
| `pov-evaluar` | Auditar caps/relato; no modifica esquema |
| `sugerencia-capitulos` | Tras esquema, escaleta cronológica |
| `guarda-analisis` | Tras `analisis_trama.md` |
| `sinopsis` | No escribir desde aquí |
