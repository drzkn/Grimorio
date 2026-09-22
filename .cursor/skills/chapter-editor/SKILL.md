---
name: chapter-editor
description: Analiza un capítulo concreto de un relato de fantasía como editor profesional. Evalúa estructura, personajes, worldbuilding, hilos de trama, coherencia con lore y caps previos, prosa, ritmo, diálogos y magia. Genera informe estructurado más anotaciones inline. Úsalo cuando el usuario diga "analiza este capítulo", "revisa el capítulo X", "feedback del capítulo", "critica el capítulo", "feedback editorial", "revisa como editor", "analiza este relato" o quiera análisis focalizado en un capítulo. No analiza ni puntúa la novela completa.
---

# Chapter Editor

Analizar un capítulo concreto de un relato de fantasía como editor profesional. Respuesta siempre en **español**.

## Flujo de trabajo

1. **Preguntar qué relato analizar**: "¿De qué relato quieres que analice un capítulo?" — esperar respuesta del usuario.
2. **Preguntar qué capítulo analizar**: "¿Qué capítulo quieres que analice? (número, nombre o título)" — esperar respuesta del usuario.
   - Si el usuario pide analizar el relato entero, "feedback editorial" o "revisa como editor" **sin** número de cap: no hacer pasada de obra ni nota del relato. Preguntar qué capítulo. Esta skill no puntúa la novela completa.
3. **Localizar la carpeta del relato**: buscar en el proyecto una carpeta cuyo nombre coincida, teniendo en cuenta que las carpetas pueden estar en snake_case o camelCase. Usar Glob o búsqueda por nombre. Si hay varias candidatas, presentarlas y pedir confirmación.
4. **Localizar el capítulo**:
   - Primero buscar un fichero dedicado al capítulo en la carpeta del relato: `capitulo_1.md`, `cap1.md`, `capitulo_uno.md`, etc.
   - Si no existe fichero dedicado, leer `contenido.md` (o `contenido.txt`) y extraer la sección correspondiente al capítulo buscado (buscar por encabezado `# Capítulo X`, `## Capítulo X`, título del capítulo, etc.).
   - Si no se encuentra el capítulo, indicarlo al usuario y listar los capítulos disponibles.
5. **Leer contexto** (obligatorio para hilos y coherencia):
   - `contexto.md` si existe.
   - Si existe `contexto_global/`: leer el merge (`resumen.md`, `contexto_historia.md`, `tono_narrador.md`, `personajes/`) **y todas** las notas `contexto_global/capitulos/*.md`, no solo la del capítulo analizado. Merge = estado acumulado. Notas de otros caps = hilos abiertos/pagados y hechos ya establecidos. La nota de este cap evita re-descubrirlo; el análisis editorial sigue exigiendo el **texto fuente** de este capítulo.
   - Contrastar el capítulo contra lore y contra caps previos/siguientes documentados. Toda contradicción se cita: fragmento de este cap + hecho/regla contradicho.
6. **Analizar el capítulo completo** antes de emitir juicio.
7. **Generar anotaciones inline** sobre pasajes concretos del capítulo.
8. **Generar informe estructurado** por áreas editoriales, enfocado en el capítulo analizado.
9. **Cierre con veredicto** y prioridad de revisiones, incluyendo **nota /10**.
10. **Guardar el análisis** en `analisis_capX.md` dentro de la carpeta del relato (donde X es el número o nombre del capítulo). Si ya existe, sobreescribir.
11. **Espejar en Notion**: seguir la skill `guarda-analisis` (tipo `Edición — Cap {N}`). Padre = fila `Análisis — Cap {N}` en la BD hija `Revisiones`. Este informe = **un toggle heading**. No página suelta ni página raíz `Análisis`. No escribir en `Capitulos`.
12. **Corregir el fichero local del capítulo**: aplicar correcciones ortográficas y gramaticales directamente sobre el fichero fuente `.md`. Solo errores de ortografía y gramática — no reescribir ni cambiar el estilo, estructura ni contenido narrativo.
13. **Corregir la página de Notion del capítulo**: aplicar las mismas correcciones en la página Notion correspondiente. Ver sección "Corrección en Notion" más abajo.
14. **Capturar contexto del capítulo**: crear o actualizar `contexto_global/capitulos/<N>.md` según la skill `contexto-capitulo`.
15. **Versión 8/10**: seguir la skill `capitulo-revisado` (ítems `🎯8` / bloque «Para 8/10» → toggle `Capítulo revisado — Cap {N}`). El capítulo canónico no se reescribe.

---

## Parte 1 — Anotaciones inline

Citar fragmentos exactos del capítulo y anotar. Formato:

```
> "[fragmento citado...]"
⚠️ RITMO: La frase se alarga sin ganancia de tensión. Partir en dos.
```

Prefijos de anotación:

| Prefijo | Cuándo usarlo |
|---------|---------------|
| 🔴 CRÍTICO | Rompe inmersión, incoherencia de mundo, agujero de trama |
| 🟡 MEJORA | Oportunidad clara de potenciar el texto |
| 🟢 FUNCIONA | Pasaje que trabaja bien — señalar por qué |
| ⚠️ RITMO | Pacing, longitud de frase, densidad |
| 💬 DIÁLOGO | Voz, naturalidad, función dramática |
| 🌍 MUNDO | Worldbuilding, consistencia de reglas |
| ✨ MAGIA | Sistema mágico, coste, coherencia interna |
| 👤 PERSONAJE | Motivación, voz, arco |

Anotar **mínimo 6 pasajes**, mezclar tipos.

---

## Parte 2 — Informe editorial del capítulo

### 1. Estructura y función del capítulo
- ¿Cuál es el propósito dramático del capítulo dentro del relato?
- ¿Hay gancho de apertura? ¿Funciona?
- Curva interna del capítulo: apertura / desarrollo / cierre
- ¿El capítulo avanza trama, personaje o ambos?
- ¿El final deja al lector con ganas de continuar?

### 2. Personajes
- Protagonista: motivación en este capítulo, voz propia, evolución
- Secundarios: función, diferenciación, coherencia con el resto del relato
- Antagonista (si aparece): presencia, credibilidad

### 3. Worldbuilding
- Reglas del mundo introducidas o aplicadas en el capítulo: ¿explicitadas? ¿respetadas?
- Nivel de detalle: ¿suficiente / excesivo / insuficiente?
- Contradicciones de lore, hilos y hechos de otros caps: sección 8 (obligatoria). No dejarlas solo aquí.

### 4. Sistema de magia / poderes
- Reglas (coste, límites, origen): ¿claras en este capítulo?
- ¿La magia resuelve problemas demasiado fácilmente?
- ¿Integración orgánica en la escena?

### 5. Prosa y voz narrativa
- Tono: ¿consistente con el resto del relato? ¿apropiado al momento dramático?
- Punto de vista: ¿estable? ¿breaches detectados?
- Originalidad del lenguaje: clichés, imágenes frescas
- Densidad descriptiva: ¿equilibrada?

### 6. Ritmo y pacing
- Balance entre escenas de acción, reflexión y diálogo
- ¿Dónde pierde energía el capítulo?
- ¿Algún pasaje que sobre o falte?

### 7. Diálogos
- ¿Suenan naturales y diferenciados por personaje?
- ¿Función dramática de cada diálogo? ¿Hay diálogos puramente expositivos (infodump)?
- Etiquetas de diálogo: ¿abuso de adverbios?

### 8. Hilos y coherencia (obligatorio)

No evaluar curva planteamiento / nudo / desenlace de la **obra**. No nota /10 del relato.

- **Abre:** qué hilos o subtramas nace en este cap. Citar.
- **Paga:** qué hilos de caps previos (o de este mismo) se resuelven o avanzan aquí. Si el hilo viene de otro cap, citar ambos lados (nota o texto previo + pasaje de este cap).
- **Cuelga:** qué queda abierto. Distinguir gancho a propósito vs olvido (se planteó y este cap no lo sostiene).
- **Agujeros / contradicciones:** incoherencia de trama, regla o hecho contra `contexto.md`, merge de `contexto_global/`, o notas de otros caps. Citar el pasaje de este cap **y** el hecho contradicho. Sin cita, no hay hallazgo.
- **Mundo implícito:** si el cap sugiere un mundo más amplio del que muestra, nombrarlo como fortaleza (profundidad) o riesgo (promesa que este cap no carga).

---

## Parte 3 — Veredicto editorial

```
CAPÍTULO ANALIZADO: [número / título]
RELATO: [nombre del relato]

ESTADO: [LISTO PARA SEGUNDA VUELTA / NECESITA TRABAJO ESTRUCTURAL / PROMETEDOR PERO EARLY DRAFT]

FORTALEZAS PRINCIPALES (top 3):
1. ...
2. ...
3. ...

POTENCIAL DEL CAPÍTULO: [1-10] / 10
NOTA FINAL: [X] / 10
NOTA DEL EDITOR: [1-2 frases honestas sobre el capítulo]
```

`NOTA FINAL` = texto actual. `POTENCIAL` = nota si se aplican los `🎯8`. El potencial **es ≥ 8** salvo `ESTADO: NECESITA TRABAJO ESTRUCTURAL` (entonces el redline no promete 8; decir qué falta).

Ponderar así: sube nota el recorte de energía muerta, la gente que importa, el lore que no se desmiente, la magia con límite y el cierre que tira. Un gazapo gramatical que ya caza la corrección ortográfica **no** mueve la nota: no es `🎯8`.

### Lista de cambios accionables

Tras el bloque de veredicto, lista numerada. Orden: primero los `🎯8` (impacto de nota, mayor primero), luego el resto. Formato:

```
N. 🎯8 🔴/🟡 [ÁREA] — [qué cambiar, en una frase imperativa]
   > "[fragmento exacto del capítulo que hay que tocar]"
   → [instrucción concreta: borrar / reescribir / expandir / mover / partir] + [cómo o por qué]
```

`🎯8` = este ítem, aplicado, cierra el hueco hacia ≥8/10. Puede ir con 🔴 o con 🟡. Sin `🎯8` = queda en el informe; `capitulo-revisado` no lo toca.

Reglas:
- **Sin fragmento, no hay entrada.** Cada cambio debe citar el texto afectado con comillas exactas del capítulo.
- Si el cambio afecta a una zona amplia (varios párrafos), citar el inicio y el final: `"[inicio...]...[...final]"`.
- La instrucción `→` debe ser accionable en menos de 30 segundos: decir exactamente qué hacer, no solo qué está mal. Si hay dos opciones de autor, escribirlas y dejar la elección en «Para 8/10».
- Si dos problemas afectan al mismo fragmento, agruparlos en una sola entrada con varias instrucciones `→`.
- Incluir **todos** los problemas detectados en Parte 1 y Parte 2 (incluida la sección 8), no solo los críticos.
- Marcar `🎯8` los que de verdad suben la nota (ritmo, personaje, mundo, hilos, magia, cierre). 🔴 de prosa/grama solo si, sin él, el cap no llega a 8.

### Para 8/10 (obligatorio)

Inmediatamente después de la lista. Contrato que consume `capitulo-revisado`:

```
### Para 8/10
**Barra:** [sí ≥8/10 | no: falta trabajo estructural — …]
**Ítems:** [números 🎯8, mismo orden]
**Elecciones:** [N → opción elegida y por qué coherente con contexto_global | ninguna]
```

Una vez generado el veredicto, guardar el análisis completo (Parte 1 + Parte 2 + Parte 3) en `analisis_capX.md` dentro de la carpeta del relato (donde X es el número o identificador del capítulo). El fichero debe comenzar con:

```
# Análisis editorial: [nombre del relato] — Capítulo [X]
**Nota:** [X] / 10
---
```

Seguido del análisis completo.

---

## Tono editorial

- Honesto pero constructivo. No adular, no destruir.
- Señalar qué **funciona** además de qué falla.
- Citar texto concreto del capítulo. No hacer afirmaciones vagas.
- Si el capítulo es muy corto (<500 palabras), indicarlo y ajustar profundidad.
- Hilos, lore y caps previos: **siempre** (sección 8), con cita. No vale "el lore no cuadra" sin fragmento + hecho contradicho.

---

## Corrección ortográfica y gramatical

Reglas comunes a la corrección local y en Notion:

- Corregir errores de ortografía (tildes, mayúsculas, palabras mal escritas).
- Corregir errores gramaticales (concordancia, puntuación incorrecta, uso erróneo de verbos).
- **No tocar**: estilo, voz narrativa, estructura de frases, elecciones léxicas del autor, contenido narrativo.
- Si una frase es torpe pero gramaticalmente correcta, **no modificarla** — eso es territorio del análisis, no de la corrección.
- Al finalizar, indicar al usuario cuántas correcciones se aplicaron y de qué tipo (ej: "3 tildes, 1 coma, 1 mayúscula") y citar cuáles han sido.

---

## Corrección en Notion

Aplicar las mismas correcciones al capítulo en Notion usando `notion-update-page` con `update_content`.

### Localizar la página Notion del capítulo

1. Buscar el relato con `notion-search` (query = nombre del relato, `content_search_mode: workspace_search`).
2. Hacer `notion-fetch` de la página del relato para localizar la BD hija `Capítulos`.
3. Hacer `notion-query-database` sobre esa BD para obtener sus entradas.
4. Identificar el capítulo correcto por la propiedad `Orden` (debe coincidir con el número/nombre del capítulo analizado).
5. Hacer `notion-fetch` de esa página de capítulo para obtener el contenido actual.

### Aplicar las correcciones

Usar `notion-update-page` con `command: "update_content"` y un array de `content_updates`, donde cada elemento tiene:
- `old_str`: el fragmento exacto con el error (tal como aparece en el fetch de Notion)
- `new_str`: el mismo fragmento corregido

Una entrada por cada corrección — no agrupar múltiples errores en un solo `old_str` salvo que estén en la misma frase continua.

Si el fetch de Notion difiere ligeramente del fichero local (formato, espacios), usar el texto del fetch como referencia para `old_str`, no el del fichero local.
