# Caracterización — reglas compartidas

Carpeta [.agents/skills/recursos-escritura-creativa/caracterizacion/](.). Origen: cap. «Caracterización» (Sanderson). Usar desde la orquestadora (`SKILL.md`), `dialogo/`, `descripcion/`, `accion/`, `introspeccion/`. Respuesta al usuario en **español**.

Al persistir `caracterizacion.md` o informes: skill `wikilinks`.

## Capas (no mezclar)

| Path | Qué es | Dueño |
|------|--------|-------|
| `<ruta>/caracterizacion.md` | Canon de **uso**: convenciones de las cuatro escrituras, voces, curva, acción, introspección | Grill de esta familia |
| `<ruta>/personajes.md` | Quién (escalas, motivo, límites) | `personaje`. Solo lectura aquí |
| `<ruta>/promesas.md` | Arco prometido | PPR. Solo lectura; no reescribir |
| `<ruta>/analisis_caracterizacion.md` | Evaluación relato entero | Evaluar |
| `<ruta>/analisis_caracterizacion_cap{N}.md` | Evaluación capítulo N | Evaluar |

`<ruta>` / `nombre` / `notion_query` = `.cursor/relato-activo.md` (skill `iniciar-relato`).

Pirámide, sala blanca y curva de aprendizaje del atlas: `mundo-entrega`, no duplicar salvo anclajes ligados al POV en descripción.

## Entrada: confirmar pilares y alcance

**Siempre** antes de grill o evaluar (salvo **modo delegado** desde la orquestadora).

`AskQuestion` en un solo formulario:

1. **Pilares** (`allow_multiple: true`): `Diálogo`, `Descripción`, `Acción`, `Introspección`. Enunciado: «¿Qué pilares de caracterización quieres trabajar?».
2. **Alcance** (si no quedó claro): `Relato entero` | `Capítulo` (+ N si capítulo).
3. **Camino** (si no quedó claro): `Grill` (definir / afilar) | `Evaluar` (auditar texto escrito).

Sin ningún pilar marcado: repetir **una vez**. No asumir los cuatro.

Sesión:

- `foco` ⊆ {`dialogo`, `descripcion`, `accion`, `introspeccion`}, no vacío.
- `alcance` = `relato` | `cap {N}`.
- `camino` = `grill` | `evaluar`.

### Skill de pilar con varios pilares marcados

Si el usuario invocó un skill de pilar y marca **más de un** pilar: delegar a orquestadora `caracterizacion` con ese foco y alcance.

### Pilares fuera del foco

Leer de `caracterizacion.md`, `personajes.md`, `promesas.md` o texto. No preguntar ni puntuar.

### Dependencias

- `descripcion` y `accion` se benefician de `personajes.md` (motivo, defecto). Si no existe: avisar; ofrecer familia `personaje` o ronda mínima en grill (sin reescribir `personajes.md` sin permiso).
- `introspeccion` en evaluar de arco visible: si no hay arco en `promesas.md` ni notas en `personajes.md`, avisar; ofrecer PPR o ronda mínima («qué cambio debe notarse»).

Grill con varios pilares: frontera en orden **dialogo → descripcion → accion → introspeccion**.

## Semilla (grill)

Orden:

1. `<ruta>/caracterizacion.md` si existe.
2. `<ruta>/personajes.md` si existe.
3. `<ruta>/promesas.md` si existe.
4. `contexto_global/`, caps del relato.
5. Mensaje del escritor si no hay local.
6. Sin semilla: una pregunta («¿voz, diálogos o cap problemático?») y parar.

Hechos escritos: buscar, no preguntar al escritor.

## Fuentes (evaluar)

- Cap: texto del cap (como `chapter-editor`: `capitulo_N.md`, `capN.md`, sección en `contenido.md`). Cortar en el `---` de `## Relacionado`.
- Relato: caps disponibles + `contexto_global/` si existe.
- `caracterizacion.md`, `personajes.md`, `promesas.md` si existen.
- `contexto_global/capitulos/<N>.md` cuando aplique.

Sin cita del texto o del plan (`caracterizacion.md` / `personajes.md`), no hay hallazgo. No modificar `caracterizacion.md` en evaluar sin permiso.

## Formato ronda grill

```
❓ **Q1** — **<título>**: <hueco concreto>
➡️ <recomendación desde semilla / texto>

---

❓ **Q2** — ...
➡️ ...
```

Frontera = decisiones abiertas cuyas previas están cerradas. Una ronda = frontera entera; «sí» acepta la recomendación. Frontera vacía → resumen (pilares del foco) → confirmación → persistir.

**Tope grill:** huecos que cambian si el lector reconoce a la persona por cómo habla, mira, actúa o piensa. Quién es: `personaje`. Arco prometido: PPR. Atlas: `mundo-entrega`. Prosa: `chapter-editor`. Escaleta: `sugerencia-capitulos`. No volcar a `esquema.md`.

## Merge `caracterizacion.md`

| Pilar en foco | Secciones que puede reescribir |
|---------------|--------------------------------|
| `dialogo` | `## Convenciones` (acotaciones, gestos, dialecto, telepatía); filas `## Voces`; `## Riesgos` (diálogo) |
| `descripcion` | `## Voces` (qué nota al describir); `## Curva` si afecta remansos descriptivos; `## Riesgos` |
| `accion` | `## Acción` completa; `## Riesgos` |
| `introspeccion` | `## Introspección` completa; `## Curva` (presupuesto emocional); `## Riesgos` |

`## Convenciones` y `## Curva` globales: el pilar que los toque en grill multi o el primero en cerrarlos. Actualizar fechas.

## Merge informe caracterización

- Cap: `<ruta>/analisis_caracterizacion_cap{N}.md`
- Relato: `<ruta>/analisis_caracterizacion.md`

Reescribir solo `## Diálogo`, `## Descripción`, `## Acción`, `## Introspección` del foco; actualizar `## Resumen de notas`. Pilares no evaluados = `—`.

Cabecera `**Fuente:**` según `wikilinks`. Tras evaluar: `guarda-analisis` (clave `Caracterización — Cap {N}` o `Caracterización — Relato`).

## Tras grill

Una pregunta: «¿Evaluar un capítulo con estos criterios?» (sí → evaluar mismo foco/alcance si el escritor indica N) | **parar**. No volcado esquema. No PPR desde aquí.

## Plantilla `caracterizacion.md`

```markdown
# Caracterización: [nombre del relato]

**Estado:** borrador | vigente
**Última actualización:** YYYY-MM-DD
**Última confirmación del escritor:** YYYY-MM-DD

## Convenciones
- **Telepatía / otro idioma:** [cursiva | versalita | …]
- **Acotaciones:** [dosis; adverbios de dicción]
- **Gestos:** [pocos, ancla | muchos, subtexto]
- **Dialecto:** [espolvoreado | pasaje inundado a propósito]

## Curva
- **Emoción:** [picos y valles; qué no se queda en diez]
- **Remansos:** [fuego de campamento / equivalente]
- **Ritmo del libro:** [largo con valles | corto sostenido]

## Voces
### [Nombre]
- **Trasfondo en la dicción:** …
- **Particularidad y dosis:** …
- **Qué nota al describir:** …
- **Mentira / no fiable:** …

## Acción
- **Promesa típica de la escena:** [contar enemigos | recorrer | …]
- **Jerga:** [enseñada antes | nombre abstracto]
- **Experto de oficio:** [sí / pendiente]

## Introspección
- **Presupuesto:** [aprox. 20–30 % o estilo declarado]
- **Estilo directo:** [migas: abre / contradice / cierra]
- **Arco visible:** [pasivo→activo; recaída; interno toca externo]
- **Secuela:** [arco cerrado en este libro | primer paso ya es arco pleno]

## Riesgos
- …
```

## Plantilla informe caracterización

```markdown
# Caracterización — [Relato | Cap N]

**Fuente:** [[<relato>/capítulos/N|Capítulo N]] · [[<relato>/contexto_global/capitulos/N|Nota cap N]]
**Alcance:** relato | capítulo N
**Última evaluación:** YYYY-MM-DD

## Resumen de notas

| Pilar | Nota | Última evaluación |
|-------|------|-------------------|
| Diálogo | — o N/10 | YYYY-MM-DD o — |
| Descripción | — o N/10 | YYYY-MM-DD o — |
| Acción | — o N/10 | YYYY-MM-DD o — |
| Introspección | — o N/10 | YYYY-MM-DD o — |

## Diálogo
**Evaluado:** YYYY-MM-DD | **Nota:** N/10
### Hallazgos
- ...
### Propuestas
- ...

## Descripción
**Evaluado:** YYYY-MM-DD | **Nota:** N/10
### Hallazgos
- ...
### Propuestas
- ...

## Acción
**Evaluado:** YYYY-MM-DD | **Nota:** N/10
### Hallazgos
- ...
### Propuestas
- ...

## Introspección
**Evaluado:** YYYY-MM-DD | **Nota:** N/10
### Hallazgos
- ...
### Propuestas
- ...
```

Relato entero: `**Fuente:**` lista de caps leídos. Sin nota de cap → omitir enlace.

## Modo delegado

La orquestadora fija `foco`, `alcance`, `camino`. Skill de pilar en delegado:

- Lee su `teoria.md`.
- Aporta rama grill o criterios evaluar.
- Sin `AskQuestion`, sin ficheros, sin Notion.

## No hacer (todas las skills caracterización)

- Copiar texto literal del libro fuente privado.
- Reescribir `personajes.md`, `promesas.md` o diseñar arco PPR.
- Volcar a `esquema.md`.
- Asumir pilares sin `AskQuestion` (salvo delegado).
- Repartir capítulos (`sugerencia-capitulos`).
- Inventar citas no presentes en texto/plan.
- Grillar pirámide/curva de mundo completa → `mundo-entrega`.

## Relación con otras skills

| Skill | Uso |
|-------|-----|
| `iniciar-relato` | Primero si falta relato activo |
| `personaje` | `personajes.md`; no duplicar quién es |
| `recursor-escritura-creativa` | Arco en `promesas.md`; no invocar desde aquí |
| `guarda-analisis` | Tras informe local |
| `caracterizacion` | Orquestadora si 2–4 pilares |
| `chapter-editor` | Localizar cap; prosa general |
| `mundo-entrega` | Sala blanca / pirámide atlas |