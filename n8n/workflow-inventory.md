# n8n Workflow Inventory — Catálogo de automatizaciones

Inventario de todos los workflows n8n que JM Consulting usa internamente y que construye para clientes como assets reutilizables.

## Principio base

n8n es el ejecutor. Claude piensa, Paperclip organiza, n8n ejecuta acciones concretas. Cada workflow es un asset reutilizable con versión, owner y métricas.

---

## Organización del inventory

Dos tipos de workflows:

### Tipo A — JM internos
Corren en `n8n.jm-consulting.io` (nuestro tenant).
Automatizan nuestra operación: sales, delivery, facturación, reporting.

### Tipo B — Cliente
Se instalan en tenant del cliente (ellos pagan infra).
Son los entregables de cada implementación.

---

## Workflows internos JM

### JM-01 — Nuevo lead → CRM + notificación
**Trigger:** reply positivo detectado en Instantly.
**Pasos:**
1. Webhook de Instantly con data del reply.
2. LLM classifier (Claude) clasifica: interesado / duda / rechazo / fuera de scope.
3. Si interesado: crea lead en CRM con stage "replied".
4. Notifica al CRO agent via Paperclip issue.
5. Agenda follow-up en 24 h si no hay discovery agendado.

**Owner:** CTO.
**Frecuencia:** event-driven.
**KPI:** tiempo lead detectado → CRM < 2 min.

---

### JM-02 — Discovery call → transcript + summary
**Trigger:** call terminada en Fireflies / Otter.
**Pasos:**
1. Webhook con transcript.
2. LLM extractor (Claude) genera:
   - Resumen ejecutivo (< 200 palabras).
   - Puntos de dolor mencionados.
   - Objeciones identificadas.
   - Next steps comprometidos.
   - Señales de fit / no-fit.
3. Actualiza CRM con summary.
4. Genera draft de follow-up email para CRO review.
5. Carga todo al client pod si se agendó audit.

**Owner:** CTO + CRO.
**Frecuencia:** event-driven.
**KPI:** summary disponible < 10 min post-call.

---

### JM-03 — Onboarding nuevo cliente
**Trigger:** SOW firmado (webhook desde DocuSign / HelloSign).
**Pasos:**
1. Crea client pod en Drive / Notion desde template.
2. Crea Slack channel compartido.
3. Emite primera factura en Stripe / Wise.
4. Agenda kickoff meeting en calendar.
5. Envía welcome email al cliente con accesos y agenda.
6. Crea issues de setup en Paperclip asignados a Head of Audit y COO.
7. Notifica al CEO agent.

**Owner:** COO + CTO.
**Frecuencia:** event-driven.
**KPI:** cliente activo en todos los sistemas < 2 h de firma.

---

### JM-04 — Maintenance reporting mensual
**Trigger:** cron día 1 de cada mes a las 6 AM ET.
**Pasos:**
1. Para cada cliente en retainer activo:
   - Pull de métricas del mes (accuracy, latency, cost, incidentes).
   - Genera dashboard actualizado.
   - LLM genera resumen (wins, pending, riesgos).
   - Compara con targets del mes anterior.
2. Crea draft de Monthly Business Review por cliente.
3. Asigna a Client Success para review antes de enviar.
4. Alerta al CTO si alguna métrica fuera de rango.

**Owner:** CTO + Client Success.
**Frecuencia:** mensual.
**KPI:** 100% de clientes con MBR listo día 3 del mes.

---

### JM-05 — Weekly sales report
**Trigger:** cron viernes 16:00 ET.
**Pasos:**
1. Pull de métricas de Instantly, LinkedIn, CRM.
2. Calcula: emails enviados, replies, bookeds, closed, revenue pipeline.
3. Compara vs targets de `/sales/outbound-playbooks.md`.
4. Genera report en markdown.
5. Envía al CEO agent + Javier.

**Owner:** CRO.
**Frecuencia:** semanal.
**KPI:** report disponible viernes < 17 PM.

---

### JM-06 — Invoice follow-up automático
**Trigger:** cron día 15 y día 25 de cada mes.
**Pasos:**
1. Pull de invoices con status "sent" y > 15 días.
2. Para cada uno: envía recordatorio al cliente (template de `/paperclip/coo-instructions.md`).
3. Loggea en tracker de COO.
4. Si > 25 días sin respuesta: crea issue escalation para COO + CEO.

**Owner:** COO.
**Frecuencia:** quincenal.
**KPI:** DSO < 30 días.

---

### JM-07 — LinkedIn content scheduler
**Trigger:** cron lunes 9 AM.
**Pasos:**
1. Lee drafts aprobados en Notion por CMO.
2. Programa posts para L-M-M-V via Buffer / Typefully.
3. Confirma scheduling al CMO agent.
4. Martes y jueves: pull de engagement del post anterior y alerta al CMO.

**Owner:** CMO + CTO.
**Frecuencia:** semanal.
**KPI:** 3+ posts/semana publicados.

---

### JM-08 — Daily cost monitoring
**Trigger:** cron diario 6 AM.
**Pasos:**
1. Pull de costos de OpenAI, Anthropic, n8n cloud, Supabase.
2. Acumula por cliente y por workstream.
3. Si algún cliente > 120% del budget mensual: alerta al CTO.
4. Si suma total > 200% del budget JM: alerta a Javier.
5. Actualiza dashboard interno.

**Owner:** CTO + COO.
**Frecuencia:** diario.
**KPI:** cero overruns no detectados en < 24 h.

---

### JM-09 — Weekly pipeline hygiene
**Trigger:** cron viernes 17 PM.
**Pasos:**
1. Pull de leads en CRM con > 7 días sin actividad.
2. Para cada uno: LLM decide (re-engage / archive / escalate).
3. Ejecuta acción automática donde aplica (auto-nudge) o crea issue para CRO.
4. Loggea resumen al CEO.

**Owner:** CRO.
**Frecuencia:** semanal.
**KPI:** < 10% de pipeline stale.

---

### JM-10 — Paperclip heartbeat monitor
**Trigger:** cron diario 20 PM.
**Pasos:**
1. Pull de actividad de cada agente de Paperclip.
2. Detecta: agentes idle > 72 h con tareas pendientes, agentes con > 150% token budget.
3. Crea issue para CEO si hay anomalías.
4. Reporte semanal a Javier los domingos.

**Owner:** CTO + CEO.
**Frecuencia:** diario.
**KPI:** agentes con budget normal > 95%.

---

## Workflows típicos para clientes (assets reutilizables)

Cada uno es un template que se customiza por cliente. Esto es lo que JM vende.

### CL-001 — Lead Response Accelerator (property mgmt)
- Clasifica leads entrantes por calidad (Tier A / B / C).
- Auto-respuesta inicial personalizada con info + pregunta abierta.
- Handoff a leasing agent sólo en leads tier A o con intención alta.
- Dashboard para director de sales con tiempos y conversión.

**ROI típico**: 5-15 puntos de conversión, 90%+ respuesta < 5 min.

---

### CL-002 — Document Intelligence (accounting / legal)
- Ingesta de PDFs o documentos escaneados.
- Extracción estructurada con LLM + validación de fields críticos.
- Push a sistema de destino (QuickBooks, Xero, DMS legal).
- Queue de revisión humana para casos con baja confianza.

**ROI típico**: 60-80% de tiempo humano ahorrado.

---

### CL-003 — Customer Support Triage
- Ingesta de tickets desde email / chat / form.
- Clasificación automática por intent (billing, technical, sales, complaint).
- Respuesta sugerida con contexto de la cuenta.
- Ruteo al agente correcto.
- Escalation automático para Sev 1.

**ROI típico**: 40-50% de tickets resueltos sin humano.

---

### CL-004 — Onboarding Documents Automation
- Recopilación de documentos del cliente al firmar.
- Validación de completitud.
- Signing flow con DocuSign / HelloSign.
- Trigger de kickoff automático cuando todo está listo.

**ROI típico**: onboarding time-to-value de semanas a días.

---

### CL-005 — Financial Reporting Agent (accounting firms)
- Pull de data desde el ERP del cliente final.
- LLM genera draft de report con comentarios y variances.
- Envío a contador senior para review antes de cliente final.

**ROI típico**: 50-70% menos tiempo en reports mensuales.

---

### CL-006 — Meeting Prep Agent
- 24 h antes de cada meeting externa:
  - Pull de data del cliente (CRM, últimas interacciones, contratos).
  - LLM genera brief con contexto, temas abiertos, next steps sugeridos.
  - Envía al asistente / account lead.

**ROI típico**: calls más productivos, menos "¿qué pasó la última vez?".

---

### CL-007 — Proposal Generator
- Input: llamada discovery transcripteada + data cliente.
- LLM genera draft de propuesta con scope, pricing, timeline.
- Review humano antes de enviar.

**ROI típico**: time-to-propuesta de 3 días a 4 horas.

---

### CL-008 — Competitive Win/Loss Analyzer
- Cada cierre / pérdida:
  - Extrae razones mencionadas en calls.
  - Agrupa patrones.
  - Dashboard para sales leadership.

**ROI típico**: mejores decisiones de roadmap y positioning.

---

### CL-009 — Customer Health Monitor
- Score continuo de salud por cliente (usage, NPS, tickets, contract timing).
- Alertas proactivas para Client Success.
- Playbooks automáticos para churn risk.

**ROI típico**: churn rate reducido 20-40%.

---

### CL-010 — AI Operations Dashboard
- Layer consolidado sobre todos los workflows del cliente.
- Métricas por workstream, costo por servicio, incidentes, ROI acumulado.
- Usado para el Monthly Business Review.

**ROI típico**: visibilidad ejecutiva al 100%; decisión de seguir/pausar por data.

---

## Versionado de workflows

Cada workflow tiene:
- **ID único**: `JM-XX` o `CL-XXX`.
- **Versión semántica**: v1.0.0 (major.minor.patch).
- **Changelog**: qué cambió en cada versión.
- **Owner**: agente responsable.
- **Fecha creación y última modificación**.
- **Dependencias**: qué otros workflows / herramientas usa.
- **Documentación**: link al spec en `/n8n/`.
- **Runbook operativo**: cómo debuggear si falla.

---

## Políticas

### Antes de publicar un workflow
- [ ] Spec escrita y revisada.
- [ ] Tests con data sintética pasando.
- [ ] Rollback plan documentado.
- [ ] Feature flag (si aplica).
- [ ] Monitoreo + alertas configuradas.
- [ ] Handoff doc para operador cliente (si es CL-*).

### Durante operación
- Logs completos 30 días mínimo.
- Cost alert por workflow.
- Error rate monitoreado; > 1% error → issue automático.

### Decomissioning
- Cuando un workflow se deja de usar: archivar (no borrar) y documentar razón.

---

## Mapa de dependencias

```
Instantly ─┐
LinkedIn ──┼─> JM-01 / JM-09 ─> CRM ─> JM-02 ─> Calendly ─> Fireflies ─> JM-03 ─> Slack + Stripe + Drive
           │
           └─> CMO posts ──> JM-07

Clientes (retainer) ─> JM-04 (mensual) ─> Client Success
Finanzas ─> JM-06 ─> COO tracker
Infra JM ─> JM-08 ─> CTO alerts
```

---

## Ver también

- `/n8n/sales-engine-spec.md`
- `/n8n/support-agent-spec.md`
- `/n8n/onboarding-workflow-spec.md`
- `/n8n/maintenance-reporting-spec.md`
- `/paperclip/cto-instructions.md`
