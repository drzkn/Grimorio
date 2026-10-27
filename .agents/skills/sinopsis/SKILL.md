---
name: sinopsis
description: >-
  Afila el storyboard de la obra al estilo grill-me: parte de una sinopsis ya
  escrita (canon = página Notion Roadmap), pregunta solo los huecos en rondas,
  y al confirmar escribe Roadmap + copia local sinopsis.md. Úsalo cuando el
  usuario diga "sinopsis", "roadmap", "storyboard", "planning de la obra",
  "grill del storyboard", "afina la sinopsis" o cuando chapter-editor pida
  aplicar una confirmación del escritor sobre el plan. No reparte capítulos:
  eso es la skill sugerencia-capitulos.
---

# Sinopsis

Afilar el **storyboard** de la obra. No inventar desenlace. No entrevista en frío. No repartir capítulos ni ritmo: skill `sugerencia-capitulos`.

Respuesta al usuario en **español**.

## Capas (no mezclar)

| Path | Qué es |
|------|--------|
| Notion `Roadmap` | Canon del plan. Si choca con local, manda Notion |
| `<ruta>/sinopsis.md` | Copia local del Roadmap. Misma pareja, mismo cuerpo |
| `<ruta>/sugerencia_capitulos.md` | Guía de ritmo y caps. **Otra skill.** Esta no la escribe |
| `contexto.md` / `contexto_global/` | Mundo y lo ya escrito. Sin futuro. Esta skill no los escribe |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

## Ubicuo

Quien modifique la sinopsis modifica **las dos copias en el mismo turno**. `Roadmap` y `<ruta>/sinopsis.md` quedan con el mismo cuerpo. Un cambio solo en Notion **no está hecho**.

Caminos que escriben el plan:

- Grill, al confirmar el entendimiento común.
- Editor, si el plan manda (beat → `desviado`) o si el texto manda.
- Alta de `Roadmap`, cuando aún no existía.

Orden: escribir `Roadmap` → volcar ese mismo cuerpo a `sinopsis.md`. El turno cierra cuando el fichero local está escrito. Si el local falla, reintentar y decirlo. No dar el cambio por guardado.

Al empezar un grill o un contraste: volcar `Roadmap` sobre `sinopsis.md` **antes** de leer. Así un retoque a mano en Notion baja al repo.

`sugerencia_capitulos.md` no entra en esta pareja.

## Flujo

1. **Relato activo**: skill `iniciar-relato`.
2. **Semilla** (sección abajo).
3. **Camino**:
   - Usuario pide sinopsis / roadmap / grill / afina → **Grill**.
   - `chapter-editor` (o el usuario) dice que el texto manda sobre un desvío → **Aplicar confirmación**.
   - `chapter-editor` dice que el plan manda → marcar beat `desviado` + `Desvíos pendientes` (ubicuo: Roadmap + local). Sin grill.
4. Tras escritura: informar rutas / URL Roadmap. 2–4 líneas. No volcar el cuerpo entero al chat.
5. Tras un grill confirmado: una pregunta — «¿reparto de capítulos?» Sí → skill `sugerencia-capitulos`. No → parar. No correrla sola.

## Semilla primero

Fuentes, en este orden:

1. Cuerpo de la página Notion `Roadmap`, si tiene texto. Copiar a `sinopsis.md`. Esa copia = semilla. Un local distinto o un pegado del mensaje **no** la sustituye.
2. `<ruta>/sinopsis.md`, solo si `Roadmap` no existe o está vacío.
3. Texto que el escritor pegue en el mensaje, solo si no hay ni Notion ni local.

Si no hay ninguna: una sola pregunta («pega la primera sinopsis») y parar. Sin entrevista en frío. Lo que se confirme en esa sesión se escribe primero en `Roadmap`.

Hechos de capítulos, notas y `contexto.md`: buscarlos. No preguntarlos al escritor.

### Localizar Roadmap

1. `notion-search` (query = `notion_query` del relato activo, `content_search_mode: workspace_search`, `page_size: 5`).
2. `notion-fetch` de la página del relato.
3. Buscar hija titulada `Roadmap` (case-insensitive; hermana de Capitulos / Revisiones).
4. Si existe: `notion-fetch` de esa página. Si tiene cuerpo → volcarlo a `sinopsis.md`.
5. Si no existe: no crear aún. Crear bajo el relato con título `Roadmap` solo al guardar un plan confirmado.
6. Local y Notion distintos: **no preguntar**. Prevalece Notion; se pisa el local.

## Grill del storyboard

Mismo gesto que grill-me: árbol de decisiones, rondas, recomendación, «sí» acepta la recomendación. El árbol es el **storyboard**.

1. Leer la semilla. Marcar cada beat, arco y promesa como **cerrado** o **abierto**.
   - Cerrado = el borrador ya lo decide.
   - Abierto = hueco, contradicción interna, o choque con un capítulo ya escrito.
2. Árbol: premisa y promesa → arcos → beats del storyboard → promesas que pagan esos beats.
3. **Frontera** = decisiones abiertas cuyas previas ya están cerradas. Una ronda pregunta la frontera entera, numerada, con recomendación sacada de la propia sinopsis (y del texto escrito, si el beat ya ocurrió). Redactar cada pregunta para que «sí» acepte la recomendación.

```
❓ **Q1** — **<título>**: <hueco concreto del storyboard>
➡️ <lectura que ya sostiene la sinopsis>

---

❓ **Q2** — ...
➡️ ...
```

4. Esperar respuestas. Recalcular la frontera. Otra ronda. Una pregunta que depende de otra aún abierta → ronda siguiente.
5. **Tope**: huecos que cambian el storyboard (desenlace, destino de un arco, orden de un beat, promesa sin pago, hecho escrito que el plan no contempla). Prosa, nombres ya fijados, beats cerrados, **cuántos capítulos y ritmo**: fuera. Eso es `sugerencia-capitulos`.
6. Frontera vacía → resumir el storyboard acordado. Esperar confirmación de entendimiento común.
7. Entonces: escribir primero `Roadmap`, luego el mismo cuerpo en `sinopsis.md`. Cada cambio de plan respecto a la semilla → `Cambios de plan`. Estado → `vigente`. Fechas de actualización y confirmación = día de hoy. **No** escribir `sugerencia_capitulos.md`.

## Aplicar confirmación

Camino corto. Sin grill.

Cuando el escritor dice que **el texto manda** sobre un desvío detectado por `chapter-editor`:

1. Traer `Roadmap` → `sinopsis.md` (si hay cuerpo).
2. Actualizar el beat afectado (`cambiado` o reescribir el beat según el texto).
3. Pasar ese desvío de `Desvíos pendientes` a `Cambios de plan` (fecha, cap, antes → después).
4. Dejar el resto de desvíos intactos.
5. Escribir `Roadmap` + `sinopsis.md` (ubicuo).

Cuando el escritor dice que **el plan manda**:

1. Traer `Roadmap` → local.
2. Beat → `desviado`. Entrada en `Desvíos pendientes` (cap, qué se sale).
3. Escribir `Roadmap` + `sinopsis.md`. No reescribir el capítulo.

## Plantilla `sinopsis.md`

```markdown
# Sinopsis: [nombre]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## Premisa
[De qué va la obra, desenlace incluido. 1 párrafo.]

## Promesa al lector
[Qué pregunta cierra el libro y qué debe sentir quien llega al final.]

## Arcos
- **[Nombre]:** quiere / teme / de dónde a dónde / destino previsto

## Storyboard
| # | Beat | Tramo | Debe pasar | Aún no | Estado |
|---|------|-------|------------|--------|--------|
| 1 | ... | cap 3–4 / acto 2 / sin asignar | ... | ... | previsto / escrito / desviado / cambiado |

## Promesas
- **[Hilo]:** se abre en [tramo] / se paga en [tramo] / estado

## Cambios de plan
- YYYY-MM-DD — cap N — [beat]: antes → después. El escritor confirmó que el texto manda.

## Desvíos pendientes
- cap N — [qué se sale] — esperando confirmación
```

Estado del beat: `previsto` | `escrito` | `desviado` | `cambiado`.

Si la semilla es prosa libre, estructurarla en esta plantilla **sin añadir hechos**. Huecos explícitos → `[hueco]` hasta que el grill los cierre.

## Escribir Roadmap

Tras confirmación:

1. Localizar o crear la página hija `Roadmap` bajo el relato.
2. Un solo cuerpo: `replace_content` / equivalente con el markdown de la plantilla de sinopsis.
3. Volcar el **mismo** cuerpo a `<ruta>/sinopsis.md`.
4. Completado: fetch de Roadmap + lectura local coinciden.

## No hacer

- Inventar desenlace o beats que el escritor no confirmó.
- Preguntar hechos que están en capítulos / notas / `contexto.md`.
- Repartir capítulos, ritmo o puentes. Eso es `sugerencia-capitulos`.
- Escribir o contrastar contra `sugerencia_capitulos.md`.
- Meter el final en `contexto_global/` o en notas de capítulo.
- Dar por guardado un cambio que solo está en Notion.
- Crear `Roadmap` vacío al empezar; solo al guardar plan confirmado.
- Leer o contrastar esta skill desde `chapter-reader` / `fantasy-reader`.

## Relación con otras skills

| Skill | Qué hacer |
|-------|-----------|
| `iniciar-relato` | Primero. Relato activo |
| `sugerencia-capitulos` | Tras grill confirmado, si el escritor pide el reparto |
| `chapter-editor` | Trae Roadmap → local; contrasta; pregunta plan/texto/pendiente; llama caminos de esta skill |
| `build-context` | No lee `sinopsis.md` ni `sugerencia_capitulos.md` |
| `chapter-reader` / `fantasy-reader` | No leen estos ficheros |
