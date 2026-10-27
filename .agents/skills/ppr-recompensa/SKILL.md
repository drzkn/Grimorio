---
name: ppr-recompensa
description: >-
  Pilar recompensa (Sanderson): pago directo, expansión, sustitución. Grill o
  evaluar cap/relato. Triggers "recompensa", "recompensas", "grill de
  recompensa", "evalúa recompensa". Varios pilares → orquestadora
  promesa-progreso-recompensa.
---

# PPR — Recompensa

Reglas compartidas: [ppr-comun.md](../ppr-comun.md). Teoría: [teoria.md](teoria.md).

## Flujo autónomo

1. `iniciar-relato` si falta relato activo.
2. Entrada en `ppr-comun.md` (proponer **Recompensa**). Si marcan más pilares → `promesa-progreso-recompensa` y parar.
3. `foco` = {`recompensa`}. Comprobar dependencias (`ppr-comun.md`).
4. **Grill:** semilla, rondas, tope, confirmación y merge según `ppr-comun.md`; árbol = solo rama abajo. Leer `teoria.md`.
5. **Evaluar:** fuentes y merge informe según `ppr-comun.md`; criterios abajo.

## Rama del grill

Por cada promesa / hilo fijado:

1. Qué se entrega al lector (concreto).
2. Tipo: directa | expansión | sustitución.
3. Si sustitución: cómo se prepara el nuevo deseo en el progreso previsto.
4. **Se paga en** (tramo / cap / final).
5. Estado del hilo al cerrar.

Riesgos: sustitución sin preparar, expansión que contradice promesa, huérfanas, pago que no deriva del progreso mostrado.

Frontera: no redefinir tono ni hitos salvo lo necesario para el pago.

Tras confirmación: merge columnas recompensa y estado en `promesas.md`. Pregunta volcado sinopsis si cambió «se paga en».

## Evaluar

Leer `teoria.md` y checklist. Fuentes: `ppr-comun.md`.

### Cap N

- Pagos parciales en el cap (cita).
- ¿Acerca el cap al pago prometido?
- Coherencia con tipo previsto en plan.

### Relato

- Tipo de cada pago (directa / expansión / sustitución).
- ¿Deriva del progreso?
- Promesas rotas u huérfanas.

Nota /10. Guardar sección `## Recompensa` + `guarda-analisis`.

## Modo delegado

Solo rama del grill o criterios de evaluación. Sin entrada, sin ficheros, sin Notion.

## No hacer

Lo de `ppr-comun.md` más: no grillar solo tono/arcos en esta skill salvo delegado multpilar.
