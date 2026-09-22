---
name: build-context
description: Revisa la carpeta contexto_global/ de un relato y la actualiza incorporando los capítulos nuevos (resumen, contexto de la historia, tono del narrador y un fichero por personaje). El merge tira de las notas contexto_global/capitulos/<N>.md, no del texto fuente, salvo que falte la nota o esté desfasada. Solo crea la carpeta desde cero si no existe. Úsalo cuando el usuario diga "actualiza el contexto", "revisa el contexto global", "build-context", "construye el contexto", "genera contexto global", "crea contexto_global" o pida sincronizar el contexto acumulado con los capítulos de un relato.
---

# Build Context

Objetivo principal: **revisar la carpeta `contexto_global/` existente de un relato y actualizarla** con la información de los capítulos que aún no estén incorporados. El merge (resumen, historia, tono, personajes) se alimenta de las **notas** `contexto_global/capitulos/<N>.md`, no del texto fuente. El `.md` de `capítulos/` solo se lee si falta la nota o está desfasada (entonces se captura primero con la skill `contexto-capitulo` y después se fusiona desde esa nota). Solo si la carpeta no existe se construye desde cero. Nunca se rehace lo que ya está correcto: se actualiza de forma incremental. Respuesta siempre en **español**.

## Flujo de trabajo

1. **Identificar el relato**: si no está claro en el mensaje, preguntar "¿De qué relato quieres revisar el contexto?".
2. **Localizar la carpeta del relato**: buscar en `relatos/` una carpeta cuyo nombre coincida (snake_case o camelCase). Si varias candidatas, presentarlas y pedir confirmación.
3. **Revisar el estado actual de `contexto_global/`** (paso central): buscar la carpeta dentro de la del relato **antes de leer ningún capítulo fuente**.
   - **Si existe**: cargar el merge (`resumen.md`, `contexto_historia.md`, `tono_narrador.md`, `personajes/`). Leer la cabecera "Capítulos incluidos" para saber hasta dónde está sincronizado. Glob `contexto_global/capitulos/*.md`: esas notas son la **fuente del merge**, no un extra. No se descartan ni se rehacen el merge ni las notas al día.
   - **Si solo existe un `contexto_global.md` antiguo de una sola pieza**: migrarlo a la nueva estructura de carpeta y seguir.
   - **Si no existe nada**: solo entonces se construye desde cero.
4. **Determinar qué capítulos faltan por incorporar**: unión de notas en `contexto_global/capitulos/` y ficheros en `capítulos/`, comparada con "Capítulos incluidos" del merge.
   - Por defecto, procesar **solo los capítulos nuevos** (aún no listados en el merge). Una nota que existe y el merge no lista (ej. cap 4 capturado, historia aún en 1–3) **cuenta como capítulo nuevo**.
   - Si el usuario indicó capítulos concretos en el mensaje, usar esos.
   - Si no hay capítulos nuevos y el usuario no pidió reprocesar, informar de que el contexto ya está al día y parar.
5. **Leer `contexto.md`** si existe — worldbuilding manual del autor. Fuente de verdad para reglas de mundo, razas, magia y entidades. No contradecirlo.
6. **Preparar la fuente de cada capítulo a incorporar** (no leer el texto fuente de entrada):
   - **Nota al día** (`contexto_global/capitulos/<N>.md` existe y el `.md` fuente no es más reciente, o no hay fuente): leer **solo la nota**. Esa es la materia prima del merge. No abrir `capítulos/<N>.md`.
   - **Nota ausente o desfasada**: seguir la skill `contexto-capitulo` (leer fuente, escribir/actualizar la nota). Después fusionar **desde esa nota**, no desde el texto completo.
   - **Ni nota ni fuente**: listar y saltar.
7. **Ejecutar protocolo de coherencia** (ver sección abajo) sobre lo extraído de las notas, antes de escribir el merge.
8. **Actualizar de forma incremental** los ficheros de merge afectados: mapear secciones de cada nota (tabla abajo). Fusionar información nueva; no reescribir lo ya correcto.
9. **Guardar** solo los ficheros de merge tocados (`resumen.md`, `contexto_historia.md`, `tono_narrador.md`, `personajes/`). Actualizar cabeceras "Capítulos incluidos" y "Última actualización". No reescribir notas de `capitulos/<N>.md` que ya estaban al día. Solo se escriben notas en el paso 6, si faltaban o estaban desfasadas.
10. **Informar al usuario**: capítulos añadidos (y si vinieron de nota existente o de captura nueva), capítulos ya presentes, ficheros de merge creados o actualizados, conflictos detectados (si los hay).

### Mapa nota → merge

| Sección de `capitulos/<N>.md` | Destino en el merge |
|-------------------------------|---------------------|
| Qué pasa | `resumen.md`; línea temporal de `contexto_historia.md` |
| Personajes | `personajes/<nombre>.md` (alta si no existe; ampliar "Aparece en") |
| Mundo / magia | Worldbuilding y sistema de magia en `contexto_historia.md` |
| Tono | `tono_narrador.md` |
| Hilos (abiertos / cerrados) | Tramas activas y preguntas abiertas |
| Continuidad | Tramas; no duplicar hechos ya en línea temporal |
| Imágenes / citas clave | Solo si anclan un hecho o una incoherencia; no copiar prosa al merge |

---

## Estructura de la carpeta contexto_global/

```
contexto_global/
  resumen.md              # Resumen del relato (merge)
  contexto_historia.md    # Worldbuilding, magia, línea temporal, tramas, preguntas abiertas, notas del editor (merge)
  tono_narrador.md        # Tono y voz narrativa (guía de coherencia) (merge)
  personajes/
    <nombre>.md           # Un fichero por personaje (merge)
  capitulos/
    <N>.md                # Snapshot de ESE capítulo (qué pasó en él). Fuente del merge. Ver skill contexto-capitulo
```

Los ficheros de merge abren con cabecera común:

```markdown
**Capítulos incluidos:** [lista]
**Última actualización:** [fecha]
```

### resumen.md

```markdown
# Resumen del relato: [nombre del relato]

**Capítulos incluidos:** [lista]
**Última actualización:** [fecha]

---

[2-4 frases sobre la historia completa hasta los capítulos analizados]
```

### personajes/<nombre>.md

Un fichero por personaje, nombre en snake_case (ej. `la_vigilante.md`).

```markdown
# [Nombre del personaje]

**Aparece en:** [[contexto_global/capitulos/X|cap X]], [[contexto_global/capitulos/Y|cap Y]]

- **Rol:** protagonista / antagonista / secundario / entidad
- **Descripción física:** [rasgos relevantes para la narración]
- **Motivación:** [qué quiere, qué teme]
- **Poderes / habilidades:** [si aplica]
- **Evolución hasta cap [X]:** [estado actual del arco]
- **Relaciones clave:** [[otra_ficha|Nombre]] — [vínculo]; …
```

### Wikilinks en merge (Obsidian)

Ver [wikilinks.md](../wikilinks.md).

- **Aparece en** y **Relaciones clave**: siempre `[[wikilink]]`. Colisión `1.md` → ruta `[[contexto_global/capitulos/N|cap N]]`, nunca `[[1]]`.
- Primera mención de personaje/cap en `contexto_historia.md` / `tono_narrador.md` / `resumen.md` → wikilink. Resto, texto plano.
- `resumen.md` cierra con bloque `## Relacionado` (notas, caps fuente, fichas, tono, historia).
- Nombre de ficha = snake_case (`la_vigilante.md` → `[[la_vigilante|La Vigilante]]`).
- **Alta de ficha nueva:** avisar que el cap fuente puede necesitar relink (`contexto-capitulo`) para que la ficha no quede huérfana en el grafo.

### contexto_historia.md

```markdown
# Contexto de la historia: [nombre del relato]

**Capítulos incluidos:** [lista]
**Última actualización:** [fecha]

---

## 1. Worldbuilding

### Mundo y geografía
[Lugares, espacios y su función en la trama]

### Razas y pueblos
[Características, cultura, lengua, costumbres relevantes]

### Sistema de tiempo
[Cómo miden el tiempo las razas del relato, equivalencias]

### Entidades y poderes cósmicos
[Entidades supremas, sus roles y limitaciones conocidas]

---

## 2. Sistema de magia / poderes

### [Nombre del sistema]
- **Origen:** [cómo se obtiene / qué lo activa]
- **Niveles o variantes:** [si los hay]
- **Costes y límites:** [restricciones conocidas]
- **Quién puede usarlo:** [razas, individuos, condiciones]
- **Ejemplos vistos en capítulos:** [cap X: evento concreto]

---

## 3. Línea temporal

| Evento | Capítulo | Notas |
|--------|----------|-------|
| [evento] | cap [X] | [detalles relevantes] |

[Ordenar cronológicamente según la narrativa, no el orden de capítulos si difieren]

---

## 4. Tramas activas

| Trama | Estado | Último evento | Cap |
|-------|--------|---------------|-----|
| [nombre de la trama] | abierta / cerrada / latente | [qué pasó último] | [X] |

---

## 5. Preguntas abiertas y semillas narrativas

- [Pregunta o elemento introducido pero no resuelto]
- [Misterio, profecía, personaje mencionado pero no desarrollado]

---

## 6. Notas del editor / incoherencias detectadas

[Solo si hay contradicciones entre capítulos o con contexto.md. Si no hay ninguna, omitir sección.]
```

### tono_narrador.md

```markdown
# Tono y voz narrativa: [nombre del relato]

**Capítulos incluidos:** [lista]
**Última actualización:** [fecha]

> Guía para mantener coherencia de tono y voz a lo largo de toda la obra.

---

- **Tono general:** [descripción del registro]
- **Evolución del tono:** [cambios entre capítulos si los hay]
- **Elementos recurrentes:** [motivos, imágenes, símbolos que aparecen más de una vez]
```

---

## Protocolo de coherencia (obligatorio antes de guardar)

Al incorporar nueva información **desde las notas de capítulo**, comprobar cada uno de estos puntos:

### 1. Conflicto nuevo vs. existente
Para cada dato nuevo extraído de los capítulos, verificar si contradice algo ya registrado en `contexto_global/` o en `contexto.md`.

| Tipo de conflicto | Acción |
|-------------------|--------|
| Nuevo dato amplía o concreta uno anterior | Fusionar: actualizar la entrada con la nueva información, añadir "cap [X]" como origen |
| Nuevo dato contradice `contexto.md` del autor | Mantener la versión del autor, anotar en `contexto_historia.md` sección "Notas del editor" con la cita de la nota (o del capítulo si la nota no trae cita y hace falta) |
| Nuevo dato contradice una entrada anterior de `contexto_global/` | Anotar ambas versiones en "Notas del editor", indicar capítulos de cada una, no resolver sin confirmación del autor |
| Nuevo dato sustituye explícitamente al anterior (ej. personaje muere, trama cerrada) | Actualizar la entrada, marcar el cambio con `(hasta cap X → cap Y)` |

### 2. Capítulos ya procesados
- Si la cabecera de los ficheros de `contexto_global/` ya lista el capítulo en "Capítulos incluidos", no reprocesar salvo que el usuario lo pida.
- Si el usuario pide reprocesar un capítulo ya incluido, ejecutar el protocolo completo de coherencia sobre ese capítulo y registrar cualquier divergencia.

### 3. Nombres y grafías
- Detectar variaciones del mismo nombre (ej. "Anaruhi" / "Anaruhy") → usar la grafía más frecuente o la de `contexto.md`, anotar variante detectada. El nombre del fichero del personaje debe usar la grafía canónica.

### 4. Línea temporal
- Verificar que los nuevos eventos encajan cronológicamente con los ya registrados. Si hay saltos o ambigüedad temporal, anotarlo en "Notas del editor" de `contexto_historia.md`.

### 5. Coherencia interna del sistema de magia
- Si una nota muestra un uso de magia que excede o contradice los niveles/límites registrados, anotarlo en "Notas del editor" — puede ser una evolución del personaje o un error narrativo. Leer el `.md` fuente solo si hace falta una cita que la nota no trae.

---

## Reglas de síntesis

- **Fuente de hechos de capítulos**: las notas `contexto_global/capitulos/<N>.md`. No re-leer el texto fuente para fusionar si la nota está al día.
- **Fuente de verdad de mundo**: `contexto.md` del autor prevalece sobre lo inferido de las notas. Si una nota contradice `contexto.md`, anotarlo en "Notas del editor" de `contexto_historia.md`, no silenciarlo.
- **Actualización incremental**: si ya existe `contexto_global/`, fusionar nueva información en los ficheros de merge. No borrar entradas anteriores a menos que un capítulo nuevo las contradiga explícitamente. No rehacer notas al día.
- **Un personaje, un fichero**: cada personaje relevante vive en su propio fichero dentro de `personajes/`. Personaje nuevo → fichero nuevo.
- **Cabeceras sincronizadas**: actualizar "Capítulos incluidos" y "Última actualización" en todos los ficheros tocados.
- **Sin spoilers adelantados**: solo incluir información que el lector ya conoce en los capítulos procesados.
- **Citar capítulo de origen** para cada dato relevante — facilita trazabilidad en análisis futuros.
- **Nombres propios exactos**: grafía del autor tal cual aparece en las notas, en los capítulos (si se capturan) o en `contexto.md`.

---

## Para análisis futuros

`build-context` fusiona desde `capitulos/<N>.md`. La skill `chapter-editor` lee el merge para el estado acumulado y **todas** las notas de caps para hilos y coherencia; el análisis editorial sigue exigiendo el texto fuente.
