# Maintenance Reporting Spec — Workflow JM-04

Spec completa del workflow mensual que consolida métricas de todos los clientes en retainer, genera drafts de Monthly Business Review y alerta sobre anomalías.

## Overview

Automatiza el corazón del retainer: data de cada cliente en un formato consistente, con insights del mes, alertas sobre riesgos, y draft de comunicación ejecutiva. El Client Success agent review, ajusta, envía.

---

## Trigger

**Cron:** primer día hábil de cada mes, 6:00 AM ET.
**Scope:** todos los clientes en retainer activo (tier 1-4).
**Excluidos:** clientes en pausa, clientes con < 30 días de onboarding.

---

## Pasos del workflow

### Paso 1: Pull de data por cliente

Para cada cliente, el workflow consume:

**A. Métricas técnicas** (via dashboard / DB del cliente):
- Accuracy por workstream (mensual vs target).
- Latency p50 y p95.
- Error rate.
- Volumen procesado (requests, tickets, documentos).
- Costos API del mes (por modelo, por workstream).
- Incidentes del mes (Sev 1-4, tiempo de resolución).

**B. Métricas de negocio** (via sistema del cliente):
- KPI definido en el SOW (ej: conversion rate, response time, time-saved).
- Comparativa vs mes anterior.
- Comparativa vs baseline pre-implementación.

**C. Métricas operativas** (internas JM):
- Horas consumidas del retainer (si tier lo incluye).
- Tickets abiertos / cerrados.
- Change Orders en el mes.
- Contactos con account lead.

---

### Paso 2: Análisis y flags

**LLM (Claude) con prompt estructurado:**

```
Input:
- Data completa del cliente del mes.
- Data de los 3 meses anteriores para comparación.
- Targets del SOW.
- Retainer tier.

Output (JSON estructurado):
{
  "wins": [
    { "description": "...", "metric": "...", "delta": "..." }
  ],
  "concerns": [
    { "description": "...", "severity": "low|medium|high", "suggested_action": "..." }
  ],
  "trends": [
    { "metric": "...", "direction": "up|down|flat", "interpretation": "..." }
  ],
  "roi_update": {
    "projected_annual_benefit": "...",
    "actual_to_date": "...",
    "variance_reason": "..."
  },
  "customer_health_score": 1-100,
  "recommendations_next_month": [...]
}
```

**Reglas de flagging automático:**
- Accuracy < target por 2+ meses → health = orange.
- Error rate > 2x baseline → health = red.
- Customer satisfaction < 4 → escalation.
- API cost > 130% budget → alerta al CTO.
- Sin comunicación con sponsor cliente > 30 días → escalation a CS.
- Churn risk score > 60 → escalation a CEO.

---

### Paso 3: Draft del MBR

**Estructura del MBR (template base):**

```
# Monthly Business Review — {{Company Name}} — {{Month YYYY}}

## 1. Executive summary (30 seg)
{{LLM summary: 3-4 líneas}}

## 2. Outcomes vs targets
| Métrica | Target | Actual | Delta |
|---|---|---|---|
{{tabla de KPIs}}

## 3. Wins del mes
{{bullet list con contexto + impacto}}

## 4. Concerns y próximos pasos
{{bullet list con acción sugerida + owner}}

## 5. ROI update
- Proyectado annual: {{X}}
- Actual YTD: {{Y}}
- Variance: {{razón}}

## 6. Plan mes siguiente
{{priorities top 3}}

## 7. Questions for you
{{preguntas abiertas para el sponsor}}

---
Reviewed by: {{Client Success agent + signed off by Javier if tier 3+}}
Next MBR: {{date}}
```

---

### Paso 4: Entregables generados automáticamente

Por cada cliente:
1. **MBR doc** — Google Doc / Notion page con el draft completo.
2. **Dashboard actualizado** — link compartido con el cliente.
3. **Slide deck** (opcional, tier 3+) — PPTX con 10-12 slides.
4. **CSV de data raw** — para auditoría / data scientist del cliente.

---

### Paso 5: Routing

**A Client Success agent (siempre):**
- Notificación con link al draft del MBR.
- Deadline: review y enviar al cliente en < 2 días hábiles.

**A CEO agent (si):**
- Health < orange.
- ROI variance > 20%.
- Sponsor change o riesgo de churn.

**A CTO (si):**
- Anomalías técnicas.
- Costos fuera de budget.
- Incidente Sev 1 sin resolver.

**A Javier (si):**
- Health = red.
- Retainer en riesgo.
- Oportunidad de upsell > 10K identificada.

---

### Paso 6: Follow-up del MBR

**Post-envío del MBR al cliente:**
- Agendar meeting del MBR (15-45 min según tier).
- Si el cliente no acepta reunión en 5 días: alerta a Client Success.
- Acta del MBR meeting archivada al pod.
- Creación de issues para next month con owner y deadline.

---

## KPIs del workflow

| KPI | Target |
|---|---|
| % de clientes con MBR listo día 3 | 100% |
| % de clientes con MBR enviado día 5 | > 90% |
| % de clientes con MBR meeting agendado | > 80% |
| Tiempo de draft → envío | < 2 días hábiles |
| Errores en pull de data | 0 críticos |
| False positives en alertas | < 10% |

---

## Estructura de data por cliente

Cada cliente tiene su folder `/delivery/clients/{{company}}/mbr/`:
```
mbr/
├── 2025-11/
│   ├── raw_data.json
│   ├── analysis.json
│   ├── mbr_draft.md
│   ├── mbr_final.md
│   ├── slides.pptx (opcional)
│   └── meeting_minutes.md
├── 2025-12/
│   └── ...
└── 2026-01/
    └── ...
```

**Ventaja:** histórico completo, replay posible, auditable.

---

## Dashboard ejecutivo JM

Consolidado de todos los clientes en retainer:

| Cliente | Tier | Health | ROI delta | Últimos Sev 1 | Next MBR | Comentario |
|---|---|---|---|---|---|---|
| Client A | T3 | 🟢 | +15% | 0 | 2026-05-05 | on track |
| Client B | T2 | 🟡 | -5% | 1 | 2026-05-07 | optimization sprint necesario |
| Client C | T1 | 🟢 | +8% | 0 | 2026-05-10 | contento |

Vista para: CEO, COO, Javier.
Update: automático cada día 3 del mes.

---

## Personalización por vertical

### Property management
- KPIs clave: lead response time, conversion rate, occupancy rate, resident satisfaction.
- Benchmark comparativo con promedio de sector.

### Accounting firms
- KPIs clave: document processing accuracy, time saved per client, deadlines met.
- Reporte cuaternario incluye reconciliación de cuentas.

### Legal boutiques
- KPIs clave: case preparation time, document automation accuracy, billable hours saved.
- Cuidado con compliance: no exponer detalles de casos.

### SaaS
- KPIs clave: ticket resolution rate, auto-resolve rate, NPS delta, churn impact.
- Sección especial: feature requests recolectados del agente.

---

## Error handling

**Data del cliente no disponible:**
- Alerta a CTO: investigar rápido.
- Generar MBR parcial con flag "data missing — pending investigation".
- Nunca enviar MBR sin review humano si hay data missing.

**LLM genera análisis inconsistente** (detectado por rules engine):
- Re-run con prompt ajustado.
- Si persiste: issue al CTO para review del prompt.
- Usar template manual fallback para este mes.

**Cliente no responde a MBR enviado:**
- Reminder día +7.
- Escalation día +14.
- Revisión de health score (posible churn risk).

---

## Integración con otros workflows

### Upstream
- JM-03 (onboarding): crea el cliente en el sistema de data.
- CL-010 (AI Ops Dashboard): provee data operativa.
- Support agent (CL-003): provee métricas de tickets.

### Downstream
- JM-06 (invoice follow-up): confirma que el retainer está pago.
- JM-08 (cost monitoring): usa data de costos para alerts.
- CL-009 (health monitor): actualiza score con data del MBR.

---

## Anti-patterns

- Enviar MBR sin review humano (rompe la trust).
- MBR genérico sin contexto del cliente.
- No trackear si el cliente lo lee (open rates con tracking pixel aceptable).
- Data sin normalizar (comparaciones inválidas).
- No actuar sobre los flags (MBR como reporte pasivo).

---

## Ver también

- `/n8n/workflow-inventory.md` (JM-04)
- `/maintenance/monthly-review-template.md`
- `/maintenance/retainer-model.md`
- `/paperclip/cto-instructions.md`
- `/delivery/handoff-template.md`
