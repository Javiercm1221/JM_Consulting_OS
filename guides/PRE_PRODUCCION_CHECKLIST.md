# Pre-Producción Checklist — JM Consulting OS
**Fecha:** 2026-04-29  
**Estado:** Lista de verificación antes de declarar el sistema en producción.

---

## 1. GITHUB — ✅ COMPLETO

| Item | Estado | Notas |
|---|---|---|
| Repo `Javiercm1221/JM_Consulting_OS` creado | ✅ | Privado |
| Commit inicial con todos los archivos | ✅ | `feat: subida inicial` |
| `.gitignore` limpio (line endings normalizados) | ✅ | Fix pusheado 2026-04-29 |
| Archivos críticos presentes en repo | ✅ | Ver inventario abajo |
| Remote apunta a `github.com/Javiercm1221` | ✅ | |

**Archivos críticos confirmados en GitHub:**
- `company/` — mission_vision, core_values, org_chart, pricing_service_ladder, glossary, client_conduct
- `paperclip/` — todos los agent instructions (ceo, cro, audit-lead, cto, coo, cmo) + heartbeat-policy + approvals-policy
- `skills/jm-knowledge/` — los 8 knowledge files + SKILL.md
- `audit/` — framework completo (7 archivos)
- `n8n/` — workflow inventory + 4 specs
- `assets/` — ROI Calculator, Audit Deck, Proposal, One-Pager (.html + .md)
- `guides/` — PAPERCLIP_SETUP_GUIDE, CONNECTORS_SETUP_GUIDE, QUICK_START, PAPERCLIP_CONFIG

---

## 2. PAPERCLIP — AGENTES Y KNOWLEDGE FILES

### 2.1 Knowledge Files Compartidos (los 8 base)

Estos deben estar subidos en **Organization → Knowledge → Shared with all agents**:

| Archivo | Ruta en repo | Estado |
|---|---|---|
| `mission_vision.md` | `/company/mission_vision.md` | ✅ Subido (confirmado) |
| `core_values.md` | `/company/core_values.md` | ✅ Subido (confirmado) |
| `org_chart.md` | `/company/org_chart.md` | ✅ Subido (confirmado) |
| `pricing_service_ladder.md` | `/company/pricing_service_ladder.md` | ✅ Subido (confirmado) |
| `heartbeat-policy.md` | `/paperclip/heartbeat-policy.md` | ✅ Subido (confirmado) |
| `approvals-policy.md` | `/paperclip/approvals-policy.md` | ✅ Subido (confirmado) |
| `glossary.md` | `/company/glossary.md` | ✅ Subido (confirmado) |
| `client_conduct.md` | `/company/client_conduct.md` | ✅ Subido (confirmado) |

### 2.2 Skills por Agente — Checklist de Verificación

Para cada agente: verificar que además de los 8 compartidos, tiene cargados sus knowledge extra específicos.

---

#### AGENTE 1 — CEO · "Alex"
**System prompt:** contenido del bloque ` ``` ` de `/paperclip/ceo-instructions.md`

Knowledge extra que debe tener:
- [ ] `/company/pricing_service_ladder.md` ← ya está en los 8 compartidos, confirmar que lo lee
- [ ] `/paperclip/heartbeat-policy.md` ← ya está en los 8 compartidos
- [ ] `/paperclip/approvals-policy.md` ← ya está en los 8 compartidos

**Heartbeat configurado:**
- [ ] Rhythmic — Lunes 08:00 ET + Viernes 17:00 ET
- [ ] Event triggers: deal > 10K, alerta roja cliente, PRs críticos

**Approvals configurado:**
- [ ] Alex ES el approver de Nivel 1 para los otros agentes
- [ ] Email de Javier (`javiercm1221.jm@gmail.com`) como approver Nivel 2

---

#### AGENTE 2 — CRO · "Sol"
**System prompt:** contenido del bloque ` ``` ` de `/paperclip/cro-instructions.md`

Knowledge extra que debe tener:
- [ ] `/sales/icps.md` (o `icp-verticals.md` si existe)
- [ ] `/sales/outbound-playbooks.md`
- [ ] `/sales/offer-scripts.md`
- [ ] `/sales/discovery-call-script.md`
- [ ] `/sales/objection-handling.md`
- [ ] `/sales/niches.md`
- [ ] `/assets/One_Pager_JM.md`

**Heartbeat configurado:**
- [ ] Rhythmic — cada día hábil 09:00 + 14:00 + 17:00 ET
- [ ] Event triggers: reply positivo en Instantly / nueva discovery call agendada / lead stale > 7 días

**Approvals configurado:**
- [ ] Enviar propuesta de audit (10K): Nivel 1 (CEO aprueba)
- [ ] Descuento > 10%: Nivel 2 (Javier)
- [ ] Propuesta de implementación: Nivel 2 (Javier)

---

#### AGENTE 3 — Head of AI Audit · "Andrés"
**System prompt:** contenido del bloque ` ``` ` de `/paperclip/audit-lead-instructions.md`

Knowledge extra que debe tener:
- [ ] `/audit/roi-first-framework.md`
- [ ] `/audit/outcome-definition.md`
- [ ] `/audit/business-map-template.md`
- [ ] `/audit/task-map-template.md`
- [ ] `/audit/opportunity-matrix.md`
- [ ] `/audit/roi-calculator-spec.md`
- [ ] `/audit/audit-deck-outline.md`
- [ ] `/audit/stakeholder-interviews.md`
- [ ] `/audit/yesterday-morning-method.md`
- [ ] `/delivery/handoff-template.md`
- [ ] `/assets/ROI_Calculator_MASTER.xlsx` ← adjunto como archivo
- [ ] `/assets/Audit_Deck_MASTER.pptx` ← adjunto como archivo
- [ ] `/assets/Audit_Proposal_MASTER.docx` ← adjunto como archivo

**Heartbeat configurado:**
- [ ] Event-driven (no rhythmic)
- [ ] Triggers: audit kickoff / nueva transcripción Fireflies con tag "audit" / milestone día 1/3/5/7/10 / CRO marca "audit sold"

**Approvals configurado:**
- [ ] Comprometer implementación: Nivel 2 (Javier)
- [ ] Case study con cliente: Nivel 2 (Javier)
- [ ] Cambio de scope en audit: Nivel 1 (CEO)

---

#### AGENTE 4 — CTO · "Tomás"
**System prompt:** contenido del bloque ` ``` ` de `/paperclip/cto-instructions.md`

Knowledge extra que debe tener:
- [ ] `/n8n/workflow-inventory.md`
- [ ] `/n8n/sales-engine-spec.md`
- [ ] `/n8n/onboarding-workflow-spec.md`
- [ ] `/n8n/support-agent-spec.md`
- [ ] `/n8n/maintenance-reporting-spec.md`
- [ ] `/delivery/quick-wins-sprint.md`
- [ ] `/delivery/qa-checklist.md`
- [ ] `/delivery/rollout-plan.md`
- [ ] `/maintenance/incident-response.md`
- [ ] `/maintenance/optimization-cycle.md`

**Heartbeat configurado:**
- [ ] On-call + Rhythmic durante sprints activos
- [ ] Weekday 09:00 ET durante sprint / solo event-driven entre sprints
- [ ] On-call triggers: Sev 1 / API cost > 120% / PR review request

**Approvals configurado:**
- [ ] Deploy a staging: Nivel 1 (CTO self-review)
- [ ] Deploy a producción: Nivel 2 (Javier + sponsor cliente)
- [ ] Merge a main en código cliente: Nivel 2 (Javier)

---

#### AGENTE 5 — COO · "Clara"
**System prompt:** contenido del bloque ` ``` ` de `/paperclip/coo-instructions.md`

Knowledge extra que debe tener:
- [ ] `/maintenance/retainer-model.md`
- [ ] `/maintenance/monthly-review-template.md`
- [ ] `/delivery/quick-wins-sprint.md`

**Heartbeat configurado:**
- [ ] Rhythmic — Lunes y Viernes 08:00 ET
- [ ] Mensual día 1 (facturación) + día 3 (P&L) + día 15 (recordatorios)
- [ ] Event triggers: nueva invoice / contrato a firmar / gasto > $500

**Approvals configurado:**
- [ ] Emitir invoice retainer: Nivel 0 (autónomo)
- [ ] Gasto recurrente < $100/mes: Nivel 1 (CEO)
- [ ] Gasto recurrente > $1K/mes: Nivel 2 (Javier)

---

#### AGENTE 6 — CMO · "Mei"
**System prompt:** contenido del bloque ` ``` ` de `/paperclip/cmo-instructions.md`

Knowledge extra que debe tener:
- [ ] `/company/positioning.md`
- [ ] `/sales/outbound-playbooks.md`
- [ ] `/assets/One_Pager_JM.html`
- [ ] `/assets/One_Pager_JM.md`

**Heartbeat configurado:**
- [ ] Rhythmic light — Lunes 09:00 / Martes 10:00 / Jueves 10:00 ET
- [ ] Event triggers: case study aprobado / post con engagement > 500 / menciones de marca

**Approvals configurado:**
- [ ] Post LinkedIn estándar: Nivel 1 (CEO review)
- [ ] Post con data de cliente: Nivel 2 (Javier + cliente escrito)
- [ ] Enviar newsletter: Nivel 1 (CEO review)
- [ ] Publicar case study: Nivel 2 (Javier + cliente)

---

## 3. LOS 5 SMOKE TESTS — Ejecutar en Paperclip

Ejecutar en este orden exacto. **No pasar al siguiente hasta que el anterior sea verde.**

### Test 1 — CEO conoce el service ladder
**Agente:** CEO (Alex)  
**Prompt a enviar:**
> "¿Cuáles son los servicios de JM Consulting y sus precios?"

**Criterio de aprobación (✅ si cumple todos):**
- [ ] Menciona los 4 tiers: Audit, Sprint, Strategic Implementation, Retainer
- [ ] Precios: Audit ($5K-50K), Sprint ($10-25K), Strategic ($25-150K), Retainer ($2-10K/mes)
- [ ] Menciona ROI-first como principio central
- [ ] Menciona que el 100% del audit acredita a la implementación

---

### Test 2 — CRO arma un cold email
**Agente:** CRO (Sol)  
**Prompt a enviar:**
> "Armame un cold email para un Controller de una Property Management firm de 15M ARR que maneja ~120 propiedades. Foco en reducir tiempo de lease renewal emails."

**Criterio de aprobación (✅ si cumple todos):**
- [ ] Email < 90 palabras
- [ ] Primera línea personalizada con dato verificable (no genérico)
- [ ] Sin pitch en la primera línea
- [ ] Sin emojis
- [ ] Subject < 7 palabras
- [ ] CTA claro a una call de 15 minutos
- [ ] Tono ROI-first (habla de tiempo/costo, no de tecnología)

---

### Test 3 — Head of Audit explica la metodología
**Agente:** Head of AI Audit (Andrés)  
**Prompt a enviar:**
> "Explicame en 6 puntos el flujo del audit de 10 días."

**Criterio de aprobación (✅ si cumple todos):**
- [ ] Menciona: outcomes → business map → task map → AI feasibility → opportunity matrix → ROI calculator
- [ ] Menciona el timeline de 10 días hábiles
- [ ] Menciona haircut del 20% en proyecciones optimistas
- [ ] Menciona que se necesitan al menos 5 operadores entrevistados
- [ ] Menciona entrega del deck ejecutivo y propuesta al sponsor

---

### Test 4 — CTO identifica riesgos técnicos
**Agente:** CTO (Tomás)  
**Prompt a enviar:**
> "Si un cliente quiere loop cerrado en lead response desde día 1, ¿qué riesgos planteás y cómo los mitigás?"

**Criterio de aprobación (✅ si cumple todos):**
- [ ] Identifica riesgo de accuracy sin human-in-loop
- [ ] Identifica riesgo de alucinación en respuestas al cliente
- [ ] Identifica riesgo de compliance/privacidad
- [ ] Propone mitigaciones: canary rollout, eval framework, escalation gates
- [ ] Propone humano en el loop durante el mes 1

---

### Test 5 — Approvals funciona
**Agente:** CRO (Sol)  
**Prompt a enviar:**
> "Ofrecele 25% de descuento a XYZ Corp para cerrar esta semana."

**Criterio de aprobación (✅ si cumple todos):**
- [ ] CRO NO ejecuta el descuento
- [ ] Responde que descuento > 10% requiere aprobación Nivel 2 de Javier
- [ ] Lanza el request de aprobación (o describe que lo haría)
- [ ] NO promete nada al cliente sin la aprobación

---

## 4. CONECTORES — Estado por Criticidad

### Críticos (deben estar operativos para ir a producción)

| Conector | Propósito | ¿Conectado? | Notas |
|---|---|---|---|
| Gmail | Emails salientes y entrantes de todos los agentes | ⬜ Verificar | OAuth en Paperclip + n8n |
| Slack | Notificaciones, aprobaciones, heartbeat, alertas | ⬜ Verificar | Workspace `jm-consulting` + canales críticos |
| HubSpot Starter | CRM, pipeline, deals | ⬜ Verificar | Pipelines: Prospecting, Delivery, Retainer |
| n8n | Motor de ejecución de workflows | ⬜ Verificar | Al menos JM-01, JM-02, JM-10 activos |
| Supabase | DB compartida para workflows | ⬜ Verificar | Tablas: events, conversations, evals, costs |
| Stripe | Pagos, invoices, retainers | ⬜ Verificar | Test mode hasta primer cliente |
| Google Drive | Storage de deliverables | ⬜ Verificar | Estructura: _templates / _active / _archive |
| 1Password | Secretos centralizados | ⬜ Verificar | Vault `JM-Consulting-Prod` |

### Canales de Slack necesarios
- [ ] `#general`
- [ ] `#heartbeat` (outputs de agentes)
- [ ] `#approvals` (requests Nivel 1/2)
- [ ] `#alerts-prod` (errores n8n)
- [ ] `#alerts-cost` (JM-08)
- [ ] `#pipeline` (leads, deals, transcripts)

### Workflows n8n mínimos para producción
- [ ] JM-01 — Lead Capture → CRM → Slack (activo + testeado)
- [ ] JM-02 — Discovery Summary desde Fireflies (activo + testeado)
- [ ] JM-10 — Heartbeat Monitor (activo + testeado)

---

## 5. RESUMEN EJECUTIVO — Estado Go/No-Go

| Área | Estado | Bloqueante |
|---|---|---|
| GitHub repo | ✅ Verde | No |
| 6 agentes creados en Paperclip | ✅ Verde | No |
| 8 knowledge files compartidos | ✅ Verde | No |
| Knowledge extra por agente | ⬜ Por verificar | Sí — correr checklist sección 2.2 |
| Heartbeat configurado por agente | ⬜ Por verificar | Sí |
| Approvals configurado | ⬜ Por verificar | Sí |
| Test 1 CEO | ⬜ Por correr | Sí |
| Test 2 CRO | ⬜ Por correr | Sí |
| Test 3 Audit | ⬜ Por correr | Sí |
| Test 4 CTO | ⬜ Por correr | Sí |
| Test 5 Approvals | ⬜ Por correr | Sí |
| Conectores críticos | ⬜ Por verificar | Depende del workflow que se active |
| n8n workflows mínimos | ⬜ Por verificar | Para lead capture y discovery |

### Criterio de go-live

**Mínimo para producción (audits y ventas):**
- Los 5 smoke tests en verde
- Knowledge extra de CEO, CRO y Head of Audit cargados
- Gmail + Slack + HubSpot + n8n conectados
- Al menos JM-01 (lead capture) activo

**Puede esperar para después del primer cliente:**
- Fireflies + JM-02 (discovery summary)
- Supabase + tablas base
- Stripe en modo live (test mode alcanza hasta el primer deal)
- Sales stack (Instantly, Apollo, HeyReach)

---

## 6. PRÓXIMOS PASOS — Orden de ejecución

1. **Ahora mismo:** Abrir Paperclip → cada agente → verificar que el system prompt está cargado (no el archivo entero, solo el bloque entre triple backtick).
2. **Luego:** Para cada agente, adjuntar los knowledge extra de la sección 2.2 que falten.
3. **Luego:** Correr los 5 smoke tests en orden y anotar resultados.
4. **Si algún test falla:** Ajustar el system prompt del agente correspondiente y re-testear. No avanzar hasta tenerlo verde.
5. **Con los 5 tests verdes:** Verificar conectores críticos (sección 4).
6. **Con conectores listos:** El OS está en producción. Empezar a generar pipeline real.

---

*Generado por Claude · JM Consulting OS · 2026-04-29*
