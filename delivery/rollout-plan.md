# Rollout Plan — De pre-prod a producción total

Cómo se escala una solución desde un piloto al 100% del volumen real sin cortar la operación.

## Filosofía

> Big bang = big risk. Siempre canary, siempre reversible, siempre medido.

## Fases del rollout

```
1. Dev/staging  →  2. Canary (10-20%)  →  3. Scale-up (50%)  →  4. 100%  →  5. Estabilización
```

### Fase 1 — Dev/Staging (semana 1-2 del sprint)

- Ambiente aislado, sin impacto en prod.
- Datos sintéticos o subset histórico.
- Objetivo: validar funcionalidad y performance técnica.
- Gate para pasar a canary: todos los tests de QA pasan.

### Fase 2 — Canary (semana 2-3)

- 10-20% del volumen real enrutado a la nueva solución.
- Otros 80-90% siguen el flujo legacy.
- Feature flag para poder revertir en segundos.
- Monitoreo intensivo durante 5 días hábiles.
- Gate para pasar a scale-up: 0 incidentes críticos, accuracy ≥ target.

### Fase 3 — Scale-up (semana 3-4)

- 50% del volumen.
- Monitoreo sigue siendo diario.
- Comparación directa con el 50% legacy.
- Gate para pasar a 100%: paridad o superioridad confirmada en métrica primaria.

### Fase 4 — 100% (semana 4+)

- Todo el volumen real.
- Monitoreo diario baja a semanal.
- Legacy se mantiene como fallback 30 días más.

### Fase 5 — Estabilización (post sprint)

- Pasa a cadencia de `/maintenance/`.
- Mantiene dashboard y alertas.
- Revisión mensual de métricas.

---

## Template de plan de rollout por workstream

Archivo: `/delivery/clients/{{company}}/workstreams/{{workstream}}/rollout.md`

```markdown
# Rollout Plan — {{workstream}}
Owner: {{rol}}
Fecha arranque canary: {{date}}
Fecha target 100%: {{date}}

## Pre-requisitos
- [ ] QA checklist completa al 100% crítico y 90% total.
- [ ] Feature flag implementada y probada.
- [ ] Plan de rollback probado en staging.
- [ ] Operador cliente capacitado.
- [ ] Runbook publicado.
- [ ] Alertas activas.

## Fase Canary (Día 1-7)
- Volumen: 10%.
- Criterio selección del 10%: {{random / región X / día Y}}.
- Métricas a observar:
  - Error rate < 1%.
  - Accuracy ≥ baseline + 10%.
  - Latency p95 < 3 s.
  - User feedback ≥ 7/10.
- Dashboard: {{link}}.
- Daily check: 9 AM con owner JM + operador cliente.
- Criterio de abort: 1 incidente sev1 O 3 incidentes sev2 en 24 h O accuracy cae > 20%.

## Fase Scale-up (Día 8-14)
- Volumen: 50%.
- Mantener daily check.
- Criterio de abort: paridad con baseline perdida, o cliente reporta problema bloqueante.

## Fase 100% (Día 15-30)
- Volumen: 100%.
- Monitoreo diario → semanal luego de 7 días.
- Legacy mantenido como fallback otros 30 días.

## Rollback procedure
1. {{paso 1, ej: flip feature flag a 0%}}.
2. {{paso 2, ej: notificar operador}}.
3. {{paso 3, ej: triage en 2 h}}.

Tiempo estimado de rollback: < 10 minutos.

## Decommission del legacy
Cuando: día 30 post 100%.
Procedimiento:
1. Verificar que no hay regresiones.
2. Archivar código legacy en branch dedicated.
3. Revocar accesos a sistemas legacy innecesarios.
4. Comunicar al equipo cliente.

## Riesgos y mitigaciones
| Riesgo | Mitigación |
| | |
```

---

## Criterios de "ir" entre fases

Gate 1 → Gate 2 (Staging → Canary):
- QA pasada.
- Feature flag testeada (on/off en < 1 min).
- Plan de rollback escrito y probado.
- Sponsor cliente avisado.

Gate 2 → Gate 3 (Canary → Scale-up):
- 5 días consecutivos sin incidentes sev1.
- Accuracy en canary ≥ target.
- Feedback del operador ≥ 7/10.
- Cobertura de monitoring completa.

Gate 3 → Gate 4 (Scale-up → 100%):
- Paridad con legacy en métrica primaria.
- No regressions en métricas secundarias.
- Costo alineado con presupuesto ± 20%.

Gate 4 → Fin (100% → Estabilización):
- 2 semanas en 100% sin incidente sev1.
- Métricas de negocio mostrando lift esperado.
- Signoff del sponsor.

---

## Monitoreo activo durante rollout

### Lo que se observa cada día (durante canary + scale-up)

**Técnicas:**
- Error rate.
- Latency p50/p95/p99.
- Throughput (req/s).
- Cost per request.
- LLM provider status.

**Negocio:**
- Métrica primaria del outcome.
- Tasa de re-trabajo humano (si operador corrige el output).
- Tickets de soporte relacionados.

**Cliente:**
- NPS / satisfacción del operador (semanal).
- Comentarios en Slack compartido.

---

## Comunicación durante el rollout

### Interna JM
- Daily sync 15 min.
- Dashboard abierto todo el día.
- Canal Slack dedicado al workstream.

### Con cliente
- Daily update por escrito (email / Slack) durante canary.
- Weekly update durante scale-up y 100% primer mes.
- Monthly review al pasar a estabilización.

### Formato del daily update al cliente
```
Rollout {{workstream}} — Día {{N}}
- Volumen procesado: {{N}} (vs {{M}} baseline).
- Accuracy: {{X%}} (target {{Y%}}).
- Errores: {{N}} (0 críticos).
- Feedback del día: {{quote o resumen}}.
- Próximo paso: {{scale-up a 50% mañana / mantener 10% otro día / etc}}.
```

---

## Rollback: cuándo y cómo

### Triggers de rollback inmediato
- Incidente sev1 (sistema caído, data loss, violación compliance).
- Sponsor cliente lo pide explícitamente.
- Accuracy cae > 30% sin causa obvia en < 1 hora.

### Triggers de pausa (no rollback, pero alto)
- Error rate 2× del baseline por 1 hora.
- Feedback operador cae < 5/10.
- Costo real > 2× presupuesto.

### Procedimiento de rollback
1. Ejecutor: owner JM técnico (no el PM, para no tener cuellos de botella).
2. Comunicación: canal Slack cliente + email al sponsor dentro de 30 min.
3. Post-mortem: 24 h después, blameless. Ver `/maintenance/incident-response.md`.
4. Decisión de go/no-go para retry: dentro de 48-72 h.

---

## Escenarios típicos que observamos

### Escenario A — Canary exitoso, scale-up falla
Causa habitual: la solución no escala al volumen alto (rate limits LLM, DB, etc.).
Acción: volver a canary, dimensionar, escalar otra vez.

### Escenario B — Accuracy cae con volumen
Causa: el 10% de canary era atípico (cherry-picked).
Acción: revisar sample de canary, re-ejecutar con sample aleatorio.

### Escenario C — Operador rechaza el output
Causa: no fue capacitado / interfaz confusa / trust no construido.
Acción: pausar rollout, mejorar UX o training, reanudar.

### Escenario D — Cliente pide add-on en medio del rollout
Acción: Change Order. NO integrar durante rollout. Anotar para v1.1.

---

## Ver también

- `/delivery/qa-checklist.md` — qué se valida antes de canary
- `/delivery/quick-wins-sprint.md` — contexto del sprint
- `/delivery/change-management.md` — cambio humano durante el rollout
- `/maintenance/incident-response.md` — si algo falla en prod
