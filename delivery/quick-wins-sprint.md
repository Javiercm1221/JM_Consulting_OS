# Quick Wins Sprint — Sprint 0 de toda implementación

Estructura del primer sprint de 2-6 semanas que entrega resultados visibles rápido. **Esto es lo que convierte un audit en un contrato de 12 meses.**

## Filosofía

> El primer resultado visible manda. Si en 30 días el cliente no ve un número moverse, todo lo demás se pone en duda.

## Reglas de oro

1. **Quick win = < 6 semanas, < 25K USD, payback < 3 meses.**
2. **Se elige 1-2 quick wins, no 5.** Más concentra mejor la ejecución.
3. **Tiene que mover un número visible, no un proceso.** Outcomes como "bajé lead response de 3h a 5min" > "digitalicé el onboarding".
4. **Se mide baseline ANTES de tocar nada.** Sin baseline, no hay "quick win", hay anécdota.

---

## Template del sprint (4 semanas estándar)

### Semana 0 — Setup

- Kickoff del workstream (ver `/delivery/handoff-template.md`).
- Baseline medido (7 días de data pre-implementación).
- Accesos a sistemas del cliente activos.
- Ambiente de dev/staging creado.
- Spec técnica firmada (scope.md v1.0).

### Semana 1 — Prototipo

**Entregable:** Prototipo funcional en sandbox con datos sintéticos.

Actividades:
- Día 1-2: Setup de infraestructura (repos, secrets, LLM provider, vector DB).
- Día 3-4: Implementación del pipeline principal.
- Día 5: Demo interna + ajustes.

Checkpoint: demo interna al equipo JM. Go/no-go para semana 2.

### Semana 2 — Piloto con datos reales

**Entregable:** Prototipo corriendo sobre data real (o muestra) en ambiente no-productivo.

Actividades:
- Día 1-2: Integración con sistema del cliente (read-only si se puede).
- Día 3-4: Corrida sobre data histórica para medir accuracy / performance.
- Día 5: Session de review con operador cliente (tester principal).

Checkpoint: métrica de calidad supera umbral mínimo.

### Semana 3 — Canary rollout

**Entregable:** Workflow activo sobre 10-20% del volumen real.

Actividades:
- Día 1: Rollout controlado (feature flag, canary).
- Día 2-5: Monitoreo diario. Daily sync de 15 min.

Checkpoint: cero incidentes críticos, feedback del operador positivo.

### Semana 4 — Rollout total + medición

**Entregable:** 100% del volumen cubierto + baseline comparativo medido.

Actividades:
- Día 1-2: Scale-up a 100%.
- Día 3-4: Medición contra baseline (semana 0).
- Día 5: Presentación al sponsor con resultados.

Checkpoint: métrica objetivo movida. Caso escrito para usar en venta futura.

---

## Ejemplos de quick wins probados por vertical

### Property Management
- Auto-respuesta IA a leads web (< 5 min). Payback 2-3 meses.
- Clasificación de tickets de maintenance (emergency / standard / cosmetic). Payback 2 meses.
- Reporte semanal automático al owner. Payback 1 mes.

### Accounting
- Extracción de data de facturas (OCR + LLM). Payback 2-3 meses.
- Reconciliación asistida (sugerencias IA). Payback 3 meses.
- Draft de emails a clientes (status, deadlines). Payback 1 mes.

### Legal boutique
- Generación de draft inicial de contratos estándar. Payback 3-4 meses.
- Intake automatizado de nuevos casos (formulario IA). Payback 2-3 meses.
- Resumen de depositions / transcripts. Payback 2 meses.

### SaaS B2B
- IA para triage de tickets de support. Payback 2-3 meses.
- Onboarding guiado con agente. Payback 3 meses.
- Resumen de calls de customer success. Payback 1-2 meses.

---

## Plantilla de métricas del sprint

Archivo: `/delivery/clients/{{company}}/workstreams/{{workstream}}/metrics.md`

```markdown
# Métricas — {{workstream}}
Baseline medido: {{fecha inicio}} a {{fecha fin}} · {{N}} días

## Baseline (pre-implementación)
- Métrica primaria: {{nombre}} = {{valor}}
- Métrica secundaria 1: {{nombre}} = {{valor}}
- Métrica secundaria 2: {{nombre}} = {{valor}}
- Volumen diario promedio: {{N}}
- Horas humanas/semana involucradas: {{H}}

## Target
- Métrica primaria: {{valor target}} (cambio de {{%}})
- Deadline: semana 4.

## Resultados semanales

### Semana 1 — Prototipo
- {{métricas internas de dev}}.

### Semana 2 — Piloto
- Accuracy en muestra histórica: {{%}}
- Latency p95: {{ms}}
- Tasks exitosas / total: {{%}}

### Semana 3 — Canary
- Volumen procesado: {{N}}
- Accuracy en prod-like: {{%}}
- Incidentes: {{#}}
- Feedback operador: {{score 1-10}}

### Semana 4 — Full rollout
- Métrica primaria post: {{valor}}
- Cambio vs baseline: {{%}}
- Horas ahorradas semana: {{H}}
- USD ahorrados semana: {{valor}}
```

---

## Playbook del Daily Sync

15 minutos, de lunes a viernes durante el sprint.

Estructura:
1. Blockers de cada uno (2 min).
2. Lo que se hizo ayer (3 min).
3. Lo que se hace hoy (3 min).
4. Métricas del día anterior (4 min) — solo en semanas 2-4.
5. Decisiones pendientes (3 min).

Formato: pie de MD actualizado en `progress.md`.

```
## 2026-02-03 — Daily
- Ayer: terminé el pipeline de clasificación. 94% accuracy en sample.
- Hoy: integración con AppFolio API + testing.
- Blocker: no recibimos credenciales de AppFolio (pidiendo a Pedro).
- Decisión pendiente: ¿clasificamos también tickets de >2 años?
```

---

## Checklist de cierre del sprint

Al final de semana 4:

- [ ] Métrica primaria movida al target (o explicación escrita de por qué no).
- [ ] Runbook de operación escrito (ver `/maintenance/`).
- [ ] Dashboard de monitoreo activo.
- [ ] Alertas configuradas (pagerduty, slack o email).
- [ ] Plan de rollback probado en staging.
- [ ] Operador cliente capacitado (video + sesión 1 h).
- [ ] Spec actualizado a v1.x con cambios reales.
- [ ] Credenciales transferidas al vault cliente.
- [ ] Case study redactado (1 página) para uso futuro.
- [ ] Invoice emitida (milestone 2 o 3 según SOW).
- [ ] Sponsor firma signoff del workstream.

---

## Reglas durante el sprint

### Hacer
- **Demo cada semana.** Aunque sea 10 minutos, aunque esté feo. Momentum > perfección.
- **Medir diario.** Métrica principal en dashboard desde día 1.
- **Feedback del operador activo.** 1 llamada/semana mínimo.
- **Commit de cambios diario.** Aunque sea WIP.
- **Documentar mientras se construye.** No al final.

### No hacer
- **No sobre-ingeniar.** Quick win es MVP, no plataforma robusta.
- **No meter features nuevas en medio del sprint.** Cambios van a scope v1.1 o Change Order.
- **No abrir 2 sprints en paralelo con el mismo cliente** en el primer mes. Primero uno bien, después el segundo.
- **No extender el sprint sin Change Order.** Si se atrasa, re-scoping explícito.

---

## Cuando un quick win "falla"

Si al final de semana 4 la métrica no se movió o se movió poco:

1. No mentir. Presentar resultados reales.
2. Diagnosticar honestamente (3 causas).
3. Presentar opciones:
   - Opción A: iterar 2 semanas más con ajuste X.
   - Opción B: descartar este quick win, pivot a otro del matrix.
   - Opción C: aceptar resultado parcial y pasar al big swing.
4. Sponsor decide.

**Un quick win fallido con honestidad crea más confianza que uno exitoso con humo.**

---

## Output del sprint

Al cierre:
- Activos técnicos en producción.
- Métricas documentadas.
- Case study redactado.
- Cliente con un resultado visible para mostrar internamente.
- JM con caso real para vender al próximo prospecto.

## Ver también

- `/delivery/implementation-scope.md` — definición de scope
- `/delivery/qa-checklist.md` — validación técnica
- `/delivery/rollout-plan.md` — rollout más allá del quick win
- `/delivery/change-management.md` — gestión del cambio humano
- `/maintenance/monthly-review-template.md` — qué sigue después del sprint
