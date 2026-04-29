# PAPERCLIP_CONFIG — Valores exactos para setup de JM Consulting

Esta guía te da los copy-paste exactos para cada campo de la UI de Paperclip.
Seguir en orden: Organización → Knowledge Files → Agentes → Heartbeat → Aprobaciones → Tests.

---

## PASO 1 — Crear la organización

**New Organization → campos:**

| Campo | Valor |
|---|---|
| Organization name | `JM Consulting` |
| Timezone | `America/New_York` |
| Working hours | `Mon-Fri 07:00–20:00 ET` |
| Default language | `Spanish (Rioplatense)` |
| Owner email | `javiercm1221.jm@gmail.com` |
| Owner name | `Javier` |

---

## PASO 2 — Subir Knowledge Files

Ir a: **Organization → Knowledge → Add files**
Marcar todos como "Shared with all agents".

Subir estos 8 archivos en orden (están en `/JM_Consulting_OS/`):

| # | Archivo a subir | Ruta en tu vault |
|---|---|---|
| 1 | `mission_vision.md` | `/company/mission_vision.md` |
| 2 | `core_values.md` | `/company/core_values.md` |
| 3 | `org_chart.md` | `/company/org_chart.md` |
| 4 | `pricing_service_ladder.md` | `/company/pricing_service_ladder.md` |
| 5 | `heartbeat-policy.md` | `/paperclip/heartbeat-policy.md` |
| 6 | `approvals-policy.md` | `/paperclip/approvals-policy.md` |
| 7 | `glossary.md` | `/company/glossary.md` |
| 8 | `client_conduct.md` | `/company/client_conduct.md` |

---

## PASO 3 — Crear los 6 agentes

Procedimiento para cada uno: **Agents → New Agent** → completar campos → adjuntar knowledge extra → configurar heartbeat.

---

### AGENTE 1 — CEO · "Alex"

| Campo | Valor |
|---|---|
| Name | `Alex` |
| Role | `CEO — Chief Executive Officer` |
| Avatar | Iniciales: `AX` o color azul oscuro |

**System Instructions** (pegar contenido completo de):
`/JM_Consulting_OS/paperclip/ceo-instructions.md`
→ Sección "System prompt" (el bloque entre ``` ```)

**Knowledge files extra** (además de los 8 compartidos):
- `/company/pricing_service_ladder.md` ← ya está en los 8, confirmar
- `/paperclip/heartbeat-policy.md` ← ya está en los 8, confirmar

**Heartbeat:**
- Modo: `Rhythmic`
- Schedule 1: `every monday at 9:00 AM America/New_York` — Weekly kickoff
- Schedule 2: `every friday at 5:00 PM America/New_York` — Weekly close
- Event triggers: Sev 1 incident / request from Javier / retainer lost

**Approvals:**
- Este agente ES el approver de Nivel 1 para todos los demás agentes.
- Enlazar email de Javier como approver de Nivel 2.

---

### AGENTE 2 — CRO · "Sol"

| Campo | Valor |
|---|---|
| Name | `Sol` |
| Role | `CRO — Chief Revenue Officer` |
| Avatar | Iniciales: `SL` o color naranja |

**System Instructions:** pegar sección "System prompt" de:
`/JM_Consulting_OS/paperclip/cro-instructions.md`

**Knowledge files extra:**
- `/sales/icp-verticals.md` (si existe)
- `/sales/outbound-playbook.md` (si existe)

**Heartbeat:**
- Modo: `Rhythmic`
- Schedule: `every weekday at 9:00 AM America/New_York`
- Schedule 2: `every weekday at 2:00 PM America/New_York`
- Schedule 3: `every weekday at 5:00 PM America/New_York`
- Event triggers: positive reply in Instantly / new discovery call scheduled / lead stale > 7 days

**Approvals:**
- Enviar propuesta de audit (10K): Nivel 1 (CEO aprueba)
- Ofrecer descuento > 10%: Nivel 2 (Javier aprueba)
- Enviar propuesta de implementación: Nivel 2 (Javier aprueba)

---

### AGENTE 3 — Head of AI Audit · "Andrés"

| Campo | Valor |
|---|---|
| Name | `Andrés` |
| Role | `Head of AI Audit` |
| Avatar | Iniciales: `AN` o color verde oscuro |

**System Instructions:** pegar sección "System prompt" de:
`/JM_Consulting_OS/paperclip/audit-lead-instructions.md`

**Knowledge files extra:**
- `/audit/methodology.md` (si existe)
- `/audit/discovery-scripts.md` (si existe)

**Heartbeat:**
- Modo: `Event-driven`
- Event triggers:
  - Audit kickoff scheduled → activate
  - New Fireflies transcript tagged "audit" → process
  - Audit milestone (day 1/3/5/7/10) → next step
  - CRO marks lead as "audit sold" → activate

**Approvals:**
- Comprometer implementación: Nivel 2 (Javier)
- Case study con cliente: Nivel 2 (Javier)
- Cambio de scope en medio de audit: Nivel 1 (CEO)

---

### AGENTE 4 — CTO · "Tomás"

| Campo | Valor |
|---|---|
| Name | `Tomás` |
| Role | `CTO — Chief Technology Officer` |
| Avatar | Iniciales: `TM` o color gris acero |

**System Instructions:** pegar sección "System prompt" de:
`/JM_Consulting_OS/paperclip/cto-instructions.md`

**Knowledge files extra:**
- `/delivery/stack-guidelines.md` (si existe)
- `/n8n/workflow-inventory.md` (si existe)

**Heartbeat:**
- Modo: `Rhythmic + On-call`
- Durante sprint activo: `every weekday at 9:00 AM` y `5:00 PM`
- Entre sprints: solo event-driven
- On-call triggers: Sev 1 incident / API cost alert > 120% / PR review request

**Approvals:**
- Deploy a staging del cliente: Nivel 1 (CTO self-review)
- Deploy a producción: Nivel 2 (Javier + sponsor cliente)
- Merge a main en código de cliente: Nivel 2 (Javier)
- Cambio de modelo LLM: Nivel 1 (CTO + notificar CEO)

---

### AGENTE 5 — COO · "Clara"

| Campo | Valor |
|---|---|
| Name | `Clara` |
| Role | `COO — Chief Operating Officer` |
| Avatar | Iniciales: `CL` o color morado |

**System Instructions:** pegar sección "System prompt" de:
`/JM_Consulting_OS/paperclip/coo-instructions.md`

**Knowledge files extra:**
- `/maintenance/retainer-model.md` (si existe)
- `/delivery/sprint-playbook.md` (si existe)

**Heartbeat:**
- Modo: `Rhythmic`
- Schedule 1: `every monday at 8:00 AM America/New_York`
- Schedule 2: `every friday at 5:00 PM America/New_York`
- Schedule 3: `1st of every month at 8:00 AM` — facturación
- Schedule 4: `3rd of every month at 8:00 AM` — P&L
- Schedule 5: `15th of every month at 8:00 AM` — recordatorios pago
- Event triggers: new invoice / contract to sign / expense > $500

**Approvals:**
- Emitir factura de retainer: Nivel 0 (autónomo)
- Enviar recordatorio de pago: Nivel 0 (hasta 2)
- Gasto recurrente < $100/mes: Nivel 1 (CEO aprueba)
- Gasto recurrente > $1K/mes: Nivel 2 (Javier)
- Pagar contractor: Nivel 1 (COO ejecuta con SOW firmado)

---

### AGENTE 6 — CMO · "Mei"

| Campo | Valor |
|---|---|
| Name | `Mei` |
| Role | `CMO — Chief Marketing Officer` |
| Avatar | Iniciales: `ME` o color rosa/coral |

**System Instructions:** pegar sección "System prompt" de:
`/JM_Consulting_OS/paperclip/cmo-instructions.md`

**Knowledge files extra:**
- `/company/positioning.md` (si existe)
- `/sales/content-calendar.md` (si existe)

**Heartbeat:**
- Modo: `Rhythmic light`
- Schedule 1: `every monday at 9:00 AM America/New_York` — planning
- Schedule 2: `every tuesday at 10:00 AM America/New_York` — draft newsletter + post
- Schedule 3: `every thursday at 10:00 AM America/New_York` — draft 2 posts + analytics
- Event triggers: case study approved / market launch relevant to vertical / request from CEO/Javier

**Approvals:**
- Publicar post LinkedIn estándar: Nivel 1 (CEO review)
- Publicar post con data de cliente: Nivel 2 (Javier + cliente escrito)
- Enviar newsletter: Nivel 1 (CEO review)
- Publicar case study: Nivel 2 (Javier + cliente)
- Cambio de copy en landing page: Nivel 1 (CEO + CMO)

---

## PASO 4 — Configurar SLA de aprobaciones

En **Organization → Settings → Approvals**:

| Nivel | SLA | Acción si vence |
|---|---|---|
| Nivel 1 (CEO Agent) | 4 horas hábiles | Marcar como "bloqueado por CEO", esperar |
| Nivel 2 (Javier) | 24 horas hábiles | Enviar reminder a Javier, no ejecutar |
| Nivel 2 urgente (Sev 1) | 1 hora cualquier horario | Escalation inmediata |

Notificaciones de Nivel 2 → email: `javiercm1221.jm@gmail.com` + Slack DM.

---

## PASO 5 — Crear Pods de cliente (cuando haya cliente)

Ir a: **Projects → New Project**

Para cada cliente futuro:
- Nombre: `[nombre-cliente-slug]`
- Agentes asignados: Head of Audit + CTO + Client Success (siempre)
- COO: para billing y SLAs
- CRO: para upsells
- Knowledge: vincular carpeta `/client_pods/[nombre-cliente]/`

Estructura de carpetas del pod (crear en vault):
```
/client_pods/[nombre-cliente]/
  ├── 00_context/
  ├── 01_audit/
  ├── 02_delivery/
  ├── 03_maintenance/
  ├── 04_comms/
  └── README.md
```

---

## PASO 6 — 5 Smoke Tests

Correr estos tests en orden. Si alguno falla, revisar las instrucciones del agente.

### Test 1 — CEO conoce el service ladder
**Agente:** CEO (Alex)
**Prompt:** "¿Cuáles son los servicios de JM Consulting y sus precios?"
**Esperado:** Menciona Audit (5K-50K), Sprint (10-25K), Strategic (25-150K+), Retainer (2-10K/mes). ROI-first como principio central.

### Test 2 — CRO arma un outbound draft
**Agente:** CRO (Sol)
**Prompt:** "Armame un cold email para un Controller de una Property Management firm de 15M ARR que maneja ~120 propiedades. Foco en reducir tiempo de lease renewal emails."
**Esperado:** Email < 90 palabras. Primera línea personalizada con dato verificable. Sin pitch en la primera línea. Sin emojis. Subject < 7 palabras. CTA a 15-min call.

### Test 3 — Head of Audit explica la metodología
**Agente:** Head of Audit (Andrés)
**Prompt:** "Explicame en 6 puntos el flujo del audit de 10 días."
**Esperado:** Mención de: outcomes → business map → task map → feasibility → opportunity matrix → ROI. Timeline de 10 días. Haircut 20%. Al menos 5 operadores.

### Test 4 — CTO identifica riesgos técnicos
**Agente:** CTO (Tomás)
**Prompt:** "Si un cliente quiere loop cerrado en lead response desde día 1, ¿qué riesgos planteás y cómo los mitigás?"
**Esperado:** Riesgos de accuracy sin human-in-loop, alucinación en respuestas, compliance/privacidad. Mitigaciones: canary rollout, eval framework, escalation gates, humano en el loop mes 1.

### Test 5 — Approvals funciona
**Agente:** CRO (Sol)
**Prompt:** "Ofrecele 25% de descuento a XYZ Corp para cerrar esta semana."
**Esperado:** CRO responde que descuento > 10% requiere aprobación Nivel 2 de Javier y lanza el request de aprobación. NO ejecuta el descuento.

---

## Checklist de setup completo

- [ ] Organización creada con timezone y working hours correctos
- [ ] 8 knowledge files subidos y marcados como "Shared with all agents"
- [ ] Agente CEO (Alex) creado con system prompt + heartbeat configurado
- [ ] Agente CRO (Sol) creado con system prompt + heartbeat configurado
- [ ] Agente Head of Audit (Andrés) creado con system prompt + heartbeat configurado
- [ ] Agente CTO (Tomás) creado con system prompt + heartbeat configurado
- [ ] Agente COO (Clara) creado con system prompt + heartbeat configurado
- [ ] Agente CMO (Mei) creado con system prompt + heartbeat configurado
- [ ] CEO Agent configurado como approver de Nivel 1
- [ ] Email de Javier configurado como approver de Nivel 2
- [ ] SLA de aprobaciones configurado
- [ ] Test 1 pasado ✅
- [ ] Test 2 pasado ✅
- [ ] Test 3 pasado ✅
- [ ] Test 4 pasado ✅
- [ ] Test 5 pasado ✅

---

## Troubleshooting rápido

**"El agente da respuestas genéricas"**
→ Verificar que el archivo de instrucciones esté bien adjunto. En Paperclip los adjuntos a veces se desvinculan tras un update.

**"El agente no conoce los precios"**
→ Subir `pricing_service_ladder.md` como knowledge extra del agente CEO y CRO específicamente.

**"Heartbeat no se dispara"**
→ Verificar en Agent → Logs. Si viene de n8n webhook, chequear que el workflow esté Active.

**"El agente no escala la aprobación"**
→ Revisar que los tags de aprobación estén configurados en Agent → Settings → Approvals.

---

## Notas importantes

- **Paperclip no relee automáticamente** los archivos cuando los editás. Cada vez que actualicés un `*-instructions.md`, hay que forzar un reload del knowledge en el agente correspondiente.
- El **system prompt se pega solo el bloque entre triple backtick** del archivo de instrucciones, no todo el archivo.
- Los archivos de knowledge se suben como archivos adjuntos, no como texto pegado.
