# Sprint Framework — Quick Wins (4 semanas)

## Pre-sprint (antes de arrancar)

1. Recibir handoff del Head of Audit (deck + task map + opportunity matrix).
2. Revisar scope, validar feasibility final con datos reales del cliente.
3. Estimar horas reales (vs. estimación del audit — si difieren > 30%, escalar al CEO).
4. Redactar spec técnica: `scope.md` + `spec.md` en el client pod.
5. Firma del sponsor antes de arrancar.
6. Configurar dashboard de observability + alertas desde el Día 1.

## Semana 1 — Setup + prototipo

- Configurar entorno: credenciales, APIs, accesos del cliente.
- Construir prototipo funcional con datos sintéticos o sample del cliente.
- Validar que el approach técnico es correcto antes de seguir.
- Feature flag implementada (off por default).
- Documentar decisiones arquitecturales tomadas.

## Semana 2 — Piloto con data real

- Activar prototipo con datos reales del cliente (feature flag on, solo 5–10% del tráfico).
- Medir accuracy y latencia contra baseline.
- Human-in-loop activo: operador del cliente revisa cada output.
- Ajustar modelo / prompts según feedback real.
- Dashboard mostrando métricas en tiempo real.

## Semana 3 — Canary rollout

- Expandir al 20–50% del tráfico real.
- Continuar human-in-loop para casos edge.
- Si accuracy ≥ target → preparar rollout completo.
- Si accuracy < target → identificar causa raíz antes de avanzar.
- Runbook operativo escrito y validado con operador del cliente.

## Semana 4 — 100% + métricas finales

- Rollout completo (100% del tráfico).
- Medir delta vs. baseline: tiempo ahorrado, errores reducidos, revenue impactado.
- Training al operador del cliente (máximo 60 min).
- QA checklist 100% críticos, 90% totales.
- Signoff del sponsor.
- Handoff a Client Success + modo retainer.

## Checklist obligatorio del CTO por sprint

- [ ] Spec técnica firmada por sponsor
- [ ] Feature flag implementada desde día 1
- [ ] Rollback plan escrito y testeado
- [ ] Dashboard activo desde día 1
- [ ] Alertas configuradas (Slack #alerts-prod)
- [ ] Runbook operativo escrito
- [ ] Training al operador completado
- [ ] QA checklist: 100% críticos, ≥ 90% totales
- [ ] Métricas delta documentadas (baseline vs. resultado)
- [ ] Signoff sponsor obtenido
- [ ] Handoff a Client Success completado

## KPIs del CTO

| KPI | Target |
|---|---|
| Workstreams entregados en tiempo | > 85% |
| Incidentes Sev 1 por cliente/mes | < 0.5 |
| MTTA Sev 1 | < 30 min |
| MTTR Sev 1 | < 4 h |
| Accuracy post-rollout ≥ target | > 90% de workstreams |
| Costo API ≤ presupuesto + 20% | > 90% de workstreams |
| Documentación 100% actualizada | 100% |
