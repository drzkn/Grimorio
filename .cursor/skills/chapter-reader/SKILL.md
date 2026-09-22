---
name: chapter-reader
description: >-
  Lee un capítulo de un relato de fantasía como lector, no como editor. Mide
  inmersión, ganas de seguir y si la gente importa en ese capítulo. Dos modos:
  beta y aficionado. Úsalo cuando el usuario diga "lee el capítulo como lector",
  "lectura del capítulo", "beta del capítulo", "qué se siente el cap X" o
  "valora el capítulo como lector".
---

# Chapter Reader

Leer **un capítulo** como quien sigue el libro, no como quien lo edita. Oficio, prosa, estructura, lista de cambios, corrección y Notion = skill `chapter-editor`. Aquí solo experiencia de lectura.

## Prosa

El informe (chat + fichero) y cualquier pregunta de esta skill van en **español natural, frases completas, bien construidas**. El feedback es el entregable: se lee como un lector que sabe escribir, no como un resumen telegráfico.

Si el hilo está en modo caveman (`/caveman`, lite/full/ultra u otra compresión), **suspenderlo mientras corre esta skill**. Reanudar caveman solo cuando el informe esté escrito y guardado.

## Flujo

1. **Relato**: "¿De qué relato quieres que lea un capítulo?" — esperar.
2. **Capítulo**: "¿Qué capítulo? (número, nombre o título)" — esperar.
3. **Modo** si no está en el mensaje: "¿Beta (señal para el autor) o aficionado (leer por ganas, con olfato de género)?"
4. **Localizar carpeta** en `relatos/`. Nombres pueden ir snake_case o camelCase. Varias candidatas → pedir confirmación.
5. **Localizar el capítulo**:
   - `capítulos/<N>.md` o `capitulos/<N>.md` (este repo usa eso).
   - Si no: `capitulo_N.md`, `capN.md`, etc.
   - Si no: extraer la sección de `contenido.md` / `contenido.txt`.
   - Si no aparece: listar capítulos disponibles y parar.
   - **Pie `## Relacionado`:** no se lee. Aparato de autor; un lector no lo ve. No cuenta para «¿paso página?». Ver [wikilinks.md](../wikilinks.md).
6. **Memoria de lector** (solo lo que ya habría leído):
   - Caps anteriores: texto o, si existe y está al día, `contexto_global/capitulos/<n>.md` para 1..N-1.
   - **No** leer `contexto.md`, merge de mundo, ni `analisis*.md`.
   - **No** leer caps posteriores a N.
   - Si el capítulo no lo dice y los anteriores tampoco, el lector no lo sabe.
7. Leer el capítulo **entero** antes de juzgar.
8. Informe conciso (plantilla abajo) + guardar local + espejo Notion (`guarda-analisis`).

## Modos

| id | Quién |
|----|--------|
| `beta` | Compañero de autor. Devuelve señal. Recorre el capítulo en orden y marca dónde se sale, dónde se queda con ganas, qué no cuadra *como lectura*. Preguntas abiertas, no recetas de oficio. |
| `aficionado` | Mitad camino entre casual y exigente. Lee por placer. Ha leído fantasía: huele tropo y truco barato. Perdona forma torpe si la historia tira. No perdona aburrirse, perderse o que no le importe nadie. Cuenta el capítulo a un amigo. |

Default si el usuario dice "como lector" / "qué se siente" sin más: **aficionado**. "beta" / "beta reader" → **beta**. Ambos modos pedidos → dos pases, dos ficheros.

## Lente (los dos modos)

Hablar en sensación, no en oficio.

Sí: "aquí me perdí", "aquí me enganché", "no me creí a esta persona", "quería el siguiente capítulo", "me aburrí", "esto ya lo he visto".

Si sale "ritmo", "arco", "infodump", "punto de vista", "gancho de cierre" → reescribir como lo vivido.

Citar solo cuando la sensación cuelga de una línea concreta. **Citas limpias:** sin `[[wikilinks]]` — `[[ahumi|Ahumi]]` → `Ahumi`. Ver [wikilinks.md](../wikilinks.md). Informe corto: cabe en una o dos pantallas. El capítulo vive dentro del libro: si algo solo funciona porque el lector ya viene de antes, decirlo; si un recién llegado a *este* cap se perdería, también.

## Informe

```markdown
# Lectura: [nombre del relato] — Capítulo [N]
**Fuente:** [[capítulos/N|Capítulo N]] · [[contexto_global/capitulos/N|Nota cap N]]
**Modo:** beta | aficionado
**¿Paso página?** sí al momento / sí pero flojo / lo dejé
**Nota:** X/10
---

## De un tirón
[8–12 líneas. Qué sentí al leer este capítulo, en orden. Sin jerga.]

## Momentos
> "cita"
🔥/😴/❓/💔/✨ [una frase de sensación]
```

4–6 momentos, mezcla de tipos:

| Marca | Sensación |
|-------|-----------|
| 🔥 | me enganché |
| 😴 | se me cayó el libro |
| ❓ | no entendí |
| 💔 | no me importó / no me lo creí |
| ✨ | esto sí — por qué, una frase |

```markdown
## Gente
- [nombre]: me importa / me da igual / me irrita — 1 frase. Solo quien aparece o pesa en este cap.

## Al cerrar
- ¿Qué me queda?
- ¿Cojo el capítulo siguiente?
```

Cola según modo:

- **beta** — 3 preguntas al autor (huecos, ganas, gente). Lista corta "aquí me salí", en orden.
- **aficionado** — ¿se lo contaría a un amigo que lee fantasía? Si huele a receta, nombrarla en habla de lector ("ya he visto esta traición", "sabe a..."), no en ficha de tropo.

```markdown
## Nota
X/10 — [1 frase honesta]
```

## Guardar

Carpeta `relatos/<relato>/lectura/`. Crear si no existe.

- `lectura/beta_cap<N>.md` o `lectura/aficionado_cap<N>.md`
- `<N>` = número del capítulo, sin padding (`1`, `2`, `4`)
- Sobreescribir el fichero de ese modo+cap. No tocar los demás.

Fichero = exactamente el informe. Nada más.

Tras guardar el fichero, seguir la skill `guarda-analisis` (tipo `Lectura {modo} — Cap {N}`). Padre = fila `Análisis — Cap {N}` en `Revisiones`. Este informe = **un toggle heading**.

## Tono

Honesto. Ni adular ni destruir. Capítulo corto (<500 palabras): decirlo y acortar. Nota /10 de **lector** (¿paso página?), no de editor (¿está bien hecho?). Conciso ≠ telegrama: cortar grasa, no artículos ni verbos.
