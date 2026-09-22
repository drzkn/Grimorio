---
name: fantasy-reader
description: >-
  Lee un relato de fantasía como lector, no como editor. Mide inmersión, ganas
  de seguir y si la gente importa. Dos modos: beta y aficionado. Úsalo cuando
  el usuario diga "lee el relato como lector", "valoración de lector", "beta
  reader del relato", "qué se siente leer esto" o "lectura del relato".
---

# Fantasy Reader

Leer el relato **entero** como quien abre un libro, no como quien lo edita. Oficio, prosa, estructura y lista de cambios = skills `fantasy-editor` / `chapter-editor`. Aquí solo experiencia de lectura.

## Prosa

El informe (chat + fichero) y cualquier pregunta de esta skill van en **español natural, frases completas, bien construidas**. El feedback es el entregable: se lee como un lector que sabe escribir, no como un resumen telegráfico.

Si el hilo está en modo caveman (`/caveman`, lite/full/ultra u otra compresión), **suspenderlo mientras corre esta skill**. Reanudar caveman solo cuando el informe esté escrito y guardado.

## Flujo

1. **Relato**: "¿Qué relato quieres que lea?" — esperar.
2. **Modo** si no está en el mensaje: "¿Beta (señal para el autor) o aficionado (leer por ganas, con olfato de género)?"
3. **Localizar carpeta** en `relatos/`. Nombres pueden ir snake_case o camelCase. Varias candidatas → pedir confirmación.
4. **Leer el texto en orden de capítulos**, como un tirón:
   - Si hay `capítulos/*.md` o `capitulos/*.md`, leerlos por número.
   - Si no, `contenido.md` / `contenido.txt` / `contenido`.
   - En cada cap: **ignorar** el pie `## Relacionado` (no es prosa; no cuenta para «¿paso página?»). Ver [wikilinks.md](../wikilinks.md).
5. **Memoria de lector**: solo el texto del relato. **No** leer `contexto.md`, `contexto_global/`, ni `analisis*.md`. Si el texto no lo dice, el lector no lo sabe.
6. Leer de cabo a rabo **antes** de juzgar.
7. Informe conciso (plantilla abajo) + guardar local + espejo Notion (`guarda-analisis`).

## Modos

| id | Quién |
|----|--------|
| `beta` | Compañero de autor. Devuelve señal. Recorre el texto en orden y marca dónde se sale, dónde se queda con ganas, qué no cuadra *como lectura*. Preguntas abiertas, no recetas de oficio. |
| `aficionado` | Mitad camino entre casual y exigente. Lee por placer. Ha leído fantasía: huele tropo y truco barato. Perdona forma torpe si la historia tira. No perdona aburrirse, perderse o que no le importe nadie. Cuenta el libro a un amigo. |

Default si el usuario dice "como lector" / "qué se siente" sin más: **aficionado**. "beta" / "beta reader" → **beta**. Ambos modos pedidos → dos pases, dos ficheros.

## Lente (los dos modos)

Hablar en sensación, no en oficio.

Sí: "aquí me perdí", "aquí me enganché", "no me creí a esta persona", "quería saber qué pasa", "me aburrí", "esto ya lo he visto".

Si sale "ritmo", "arco", "infodump", "punto de vista", "gancho" → reescribir como lo vivido.

Citar solo cuando la sensación cuelga de una línea concreta. **Citas limpias:** sin `[[wikilinks]]` — `[[ahumi|Ahumi]]` → `Ahumi`. Ver [wikilinks.md](../wikilinks.md). Informe corto: cabe en una o dos pantallas.

## Informe

```markdown
# Lectura: [nombre del relato]
**Fuente:** [[capítulos/1|Capítulo 1]], [[capítulos/2|Capítulo 2]], … (caps leídos)
**Modo:** beta | aficionado
**¿Paso página?** sí al momento / sí pero flojo / lo dejé
**Nota:** X/10
---

## De un tirón
[8–12 líneas. Qué sentí al leer, en orden. Sin jerga.]

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
- [nombre]: me importa / me da igual / me irrita — 1 frase

## Al cerrar
- ¿Qué me queda?
- ¿Cojo otro libro de este mundo?
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

- `lectura/beta.md` o `lectura/aficionado.md`
- Sobreescribir el fichero de ese modo. No tocar el otro.

Fichero = exactamente el informe. Nada más.

Tras guardar el fichero, seguir la skill `guarda-analisis` (tipo `Lectura {modo} — Relato`). Padre = fila `Análisis — Relato` en `Revisiones`. Este informe = **un toggle heading**.

## Tono

Honesto. Ni adular ni destruir. Relato corto (<500 palabras): decirlo y acortar. Nota /10 de **lector** (¿volvería?), no de editor (¿está bien hecho?). Conciso ≠ telegrama: cortar grasa, no artículos ni verbos.
