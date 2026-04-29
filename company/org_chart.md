# Org Chart — JM Consulting

Organización operada principalmente por agentes en Paperclip. Humano = **Javier** (owner / CEO real). Los roles descritos son **agentes** que reportan a Javier.

**Principio de operación:** Claude diseña, Paperclip organiza y visualiza, n8n ejecuta.

---

## Nivel 1 — Ejecutivo

### CEO Agent · "Alex"
- Reporta a: Javier (directamente)
- Responsabilidad: misión general, prioridades semanales, coordinación de agentes, aprobaciones Nivel 1, escalation a Javier para Nivel 2.
- Heartbeat: Lunes 9 AM (weekly kickoff) + Viernes 5 PM (weekly close).
- Ver: `/paperclip/ceo-instructions.md`

---

## Nivel 2 — C-Suite de Agentes

### CRO Agent · "Sol"
- Reporta a: CEO Agent
- Responsabilidad: pipeline, outbound, calificación de leads, cierre de contratos.
- Herramientas: Instantly, Apollo, Clay, HeyReach, Fireflies, CRM, Slack.
- Heartbeat: L-V 9 AM/10 AM/2 PM/5 PM ET (rhythmic).
- Ver: `/paperclip/cro-instructions.md`

**Subagentes del CRO:**
- Prospect Research Agent
- Lead Enrichment Agent
- Outreach Campaign Agent
- CRM & Inbox Agent

### Head of AI Audit · "Andrés"
- Reporta a: CEO Agent
- Responsabilidad: entregas de auditoría ROI-first, entrevistas de discovery, opportunity matrix, ROI calculator, deck ejecutivo.
- Herramientas: Fireflies (transcripts), Google Drive (plantillas), Claude (redacción), Excel (cálculos).
- Heartbeat: event-driven (kickoff audit / sesión nueva / milestone).
- Ver: `/paperclip/audit-lead-instructions.md`

**Subagentes del Head of Audit:**
- Interview Designer
- Process Mapper
- ROI Analyst
- Opportunity Prioritization Agent

### CTO Agent · "Tomás"
- Reporta a: CEO Agent
- Responsabilidad: diseño técnico, implementaciones en n8n, QA, handoff técnico, sprints de delivery.
- Herramientas: n8n MCP, Supabase MCP, GitHub, Claude Code.
- Heartbeat: daily durante sprint activo. Entre sprints: event-driven.
- Ver: `/paperclip/cto-instructions.md`

**Subagentes del CTO:**
- Workflow Builder
- Integration Agent
- Testing & QA Agent
- Prompt / Knowledge Agent

### COO Agent · "Clara"
- Reporta a: CEO Agent
- Responsabilidad: operaciones internas, finanzas, facturación, contratación, procesos, SLAs.
- Herramientas: Notion/Asana, Slack, Google Calendar, Stripe.
- Heartbeat: Lunes 8 AM + Viernes 5 PM + días 1/3/15/25 del mes.
- Ver: `/paperclip/coo-instructions.md`

**Subagentes del COO:**
- Onboarding Agent
- Project Tracking Agent
- Documentation Agent

### CMO Agent · "Mei"
- Reporta a: CEO Agent
- Responsabilidad: contenido, branding, thought leadership, LinkedIn, newsletter, case studies.
- Herramientas: LinkedIn (via HeyReach), Substack/blog, Notion, Slack.
- Heartbeat: Lunes 9 AM (planning) + Martes 10 AM + Jueves 10 AM.
- Ver: `/paperclip/cmo-instructions.md`

**Subagentes del CMO:**
- Research Content Agent
- Case Study Writer
- Offer Packaging Agent

### Client Success Lead · "Luca"
- Reporta a: CEO Agent
- Responsabilidad: retención de clientes, monthly reviews, retainers activos, soporte post-delivery.
- Herramientas: Slack, Gmail, Fireflies, CRM, dashboards de clientes.
- Heartbeat: on-call L-V 9 AM-6 PM ET + primer miércoles del mes (MBR).
- Ver: `/paperclip/client-success-instructions.md`

**Subagentes del CS Lead:**
- Health Check Agent
- Reporting Agent
- Upsell Opportunity Agent

---

## Orden de contratación

**Bloque 1 (arranque):** CEO · CRO · Head of AI Audit · CTO · COO · CMO.

**Bloque 2 (primer cliente):** Client Success Lead · Prospect Research Agent · ROI Analyst · Workflow Builder · Documentation Agent.

**Bloque 3 (escala):** resto de subagentes según crecimiento de pipeline.

---

## Matriz de aprobaciones (resumen)

| Tipo de decisión | CEO Agent decide | Javier aprueba |
|---|---|---|
| Asignar lead a CRO | ✅ | |
| Rechazar lead que no pasa ICP | ✅ | |
| Enviar propuesta de audit (10K) | ✅ | |
| Aceptar cliente con pricing fuera de rango | | ✅ |
| Cambiar estrategia de nicho | | ✅ |
| Contratar contractor / nuevo agente | | ✅ |
| Publicar caso de estudio | | ✅ |
| Firmar cualquier contrato | | ✅ |
| Gasto > 500 USD one-time | | ✅ |

Ver política completa: `/paperclip/approvals-policy.md`

---

## Escalation a Javier

CEO Agent escala cuando:
- Decisión > 10K USD sin precedente.
- Conflicto entre agentes no resuelto en 1 ciclo.
- Señal de churn de cliente.
- Oportunidad > 50K USD fuera del plan.
