# Optimization Cycle — Ciclo de optimización trimestral

Proceso estructurado de mejora continua post-implementación. Asegura que los modelos, prompts y workflows no se degradan con el tiempo y evolucionan con el negocio del cliente.

## Filosofía

> Sin mejora continua, la IA se deteriora. El mundo cambia, el modelo no, y un año después estás procesando con lógica vieja.

## Cuándo se ejecuta

- **Tier 2**: 1 vez por trimestre.
- **Tier 3**: mensual.
- **Tier 4**: continuo (parte del trabajo diario).

Duración del ciclo: 2-3 semanas.

---

## Estructura del ciclo (5 pasos)

```
1. Data review  →  2. Hypothesis  →  3. Experiment  →
4. Evaluate  →  5. Ship or iterate
```

---

## Paso 1 — Data review (3-5 días)

### Actividades
- Pull de 90 días de logs + outputs + feedback humano.
- Tablas con:
  - Accuracy por día / semana (buscar drift).
  - Distribución de confidence scores.
  - Casos de alto error reciente.
  - Quejas del operador (si hay canal de feedback).
  - Costo promedio por transacción.
- Identificar 3-5 patterns: dónde falla, qué escenarios sufren.

### Entregable
`/delivery/clients/{{company}}/optimization/{{YYYY-Q#}}/data-review.md`

```markdown
# Data Review — {{Q}}
Período analizado: {{fecha_inicio}} a {{fecha_fin}}

## Métricas clave
- Accuracy overall: {{%}} (cambio vs Q anterior: {{%}})
- Accuracy por segmento:
  - Segmento A: {{%}}
  - Segmento B: {{%}}
- Drift detectado: {{sí/no}} — {{descripción}}

## Top 5 failure modes (ordenados por frecuencia)
1. {{descripción}} — {{N}} casos — {{costo estimado}}
2. ...

## Hallazgos
-
-

## Hipótesis para testear
1. {{si cambiamos X, mejora Y}}
2. ...
```

---

## Paso 2 — Hypothesis (2-3 días)

### Actividades
- Por cada hypothesis, definir:
  - Cambio propuesto (prompt, modelo, flujo, umbral).
  - Métrica esperada a mover.
  - Riesgo del cambio.
  - Esfuerzo de implementación.
- Priorizar: impacto esperado × facilidad.
- Elegir 1-3 experimentos para el ciclo.

### Entregable
`/delivery/clients/{{company}}/optimization/{{YYYY-Q#}}/hypotheses.md`

```markdown
# Hypotheses — {{Q}}

## H1: {{nombre}}
- Cambio: {{descripción}}.
- Métrica target: {{métrica}} +{{delta}}%.
- Grupo control: 50% del volumen.
- Grupo experimento: 50%.
- Duración: {{N}} días.
- Riesgo: {{bajo/medio/alto}} — {{mitigación}}.
- Effort: {{horas}}.

## H2: ...
```

---

## Paso 3 — Experiment (7-10 días)

### Setup
- Feature flag o routing para split traffic.
- Si el cambio es prompt: A/B test simultáneo.
- Si el cambio es modelo: canary con 10% primero, luego 50%.
- Si el cambio es flujo: piloto en un subconjunto (1 sede, 1 vertical interno).

### Ejecución
- Monitoring diario del split.
- Alerta si el experimento regression > 10% en variante test.
- Minimum sample size: 500 casos por variante (si el volumen lo permite).

---

## Paso 4 — Evaluate (2-3 días)

### Actividades
- Estadística básica: diferencia absoluta, p-value, CI 95%.
- Lectura cualitativa: revisar 20 casos de la variante ganadora (¿mejoró o cambió de una forma no deseada?).
- Check de edge cases: ¿regression en segmentos no mayoritarios?

### Entregable
```markdown
# Experiment Result — {{H1 nombre}}

## Resultado cuantitativo
- Control (n={{N}}): {{métrica}} = {{valor}} ± {{error}}.
- Test (n={{N}}): {{métrica}} = {{valor}} ± {{error}}.
- Lift: {{%}} ({{p-value}}, CI {{range}}).

## Resultado cualitativo
- Casos revisados: {{N}}.
- Mejoras claras: {{descripción}}.
- Regresiones: {{descripción}} (impacto: {{severidad}}).

## Recomendación
[ ] Ship a 100%.
[ ] Iterar (hypothesis modificada).
[ ] Descartar.

## Razón
{{justificación}}.
```

---

## Paso 5 — Ship or iterate (2-3 días)

### Si ship
- Rollout al 100% siguiendo `/delivery/rollout-plan.md` abreviado.
- Updatear documentación (spec, FAQ, runbook).
- Comunicar al cliente en monthly review.
- Documentar en `change-log.md` del workstream.

### Si iterate
- Re-definir hypothesis.
- Volver al paso 3.

### Si descartar
- Documentar por qué no funcionó.
- Re-priorizar el backlog.
- Evitar volver a probar eso sin nueva data.

---

## Tipos de optimización comunes

### Prompt engineering
- Clarificar instrucciones.
- Agregar ejemplos (few-shot).
- Reducir longitud para bajar costo sin perder accuracy.
- Segmentar: diferentes prompts para diferentes tipos de input.

### Model swap
- Probar modelo más chico (baja costo).
- Probar modelo más nuevo (sube accuracy, a veces baja latency).
- Probar proveedor alternativo (fallback).

### Retrieval tuning (para RAG)
- Ajustar chunk size.
- Mejorar embedding model.
- Rerank con modelo dedicado.
- Filtrar por metadata.

### Workflow refactor
- Eliminar pasos no agregan valor.
- Paralelizar dónde se pueda.
- Cachear respuestas frecuentes.

### Threshold tuning
- Ajustar confidence cutoffs.
- Ajustar rules de escalación a humano.
- Calibrar por segmento.

### UX del operador
- Mejorar el interfaz de revisión / override.
- Acortar el tiempo de feedback.
- Auto-sugerencias basadas en historia.

---

## Gestión del costo durante optimización

Regla: un ciclo de optimización no debería incrementar costo operativo > 20% sin autorización del cliente.

Monitorear especialmente si se prueba:
- Modelo más grande.
- Más tokens en prompt.
- Chain-of-thought o self-consistency.
- Retrieval con más chunks.

Si sube costo pero sube accuracy, presentar al cliente con el trade-off explícito.

---

## Ownership

| Rol | Responsabilidad |
|---|---|
| Account Lead JM | Prioriza + comunica al cliente |
| Technical Lead JM | Implementa + mide |
| Operador cliente | Valida cualitativamente |
| Sponsor cliente | Aprueba cambios ship |

---

## Entregable del trimestre (informe al cliente)

Al final de cada ciclo, informe de 1 página:

```markdown
# Optimization Cycle {{Q#}}/{{año}} — {{Company}}

## Experimentos ejecutados
1. {{H1 nombre}} — {{resultado}} — {{lift}}.
2. {{H2 nombre}} — {{resultado}} — {{lift}}.
3. {{H3 nombre}} — {{resultado}} — {{lift}}.

## Cambios shippeados
- {{qué}} → métrica primaria ahora {{X}} vs {{Y}} baseline.

## Aprendizajes para Q siguiente
-

## Recomendación de focos Q siguiente
1.
2.
3.
```

Se presenta en el monthly review del primer mes del siguiente Q.

---

## Anti-patterns

- **Cambiar sin medir.** Toda optimización arranca con métrica definida.
- **Experimento sin grupo control.** Si no sabés qué hubiera pasado, no aprendiste.
- **Ship sin revisar casos reales.** Los numeritos mienten si la data está mal.
- **Iterar infinito.** Si después de 2 ciclos no hay lift, descartar y probar otra cosa.
- **No comunicar los fracasos al cliente.** La transparencia construye confianza.

---

## Ver también

- `/maintenance/monthly-review-template.md` — donde se presenta el resultado
- `/maintenance/retainer-model.md` — tiers que incluyen optimization
- `/delivery/qa-checklist.md` — baseline de calidad a mantener
