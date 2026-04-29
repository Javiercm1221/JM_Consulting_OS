# Onboarding Workflow Spec — Automatización del onboarding cliente

Spec del workflow JM-03 — "Nuevo cliente onboarding". Cuando se firma un SOW, la máquina arranca sola: crea pod, agenda kickoff, emite primera factura, notifica al team.

## Overview

Reducir el tiempo desde "cliente firma" a "cliente activo y con kickoff agendado" de días a < 2 horas. Es uno de los workflows más valiosos para la operación interna de JM — también se vende como entregable (CL-004) para clientes cuyo onboarding sea lento.

---

## Trigger

**Evento:** SOW firmado.

**Fuentes posibles:**
- Webhook de DocuSign / HelloSign / PandaDoc cuando el documento cambia a "completed".
- Status change en CRM a "closed won".
- Manual trigger desde Paperclip (CEO agent marca "cliente firmado").

**Validación del trigger:**
- Verificar que el SOW tenga: cliente, scope, precio, fechas, signatarios.
- Si falta algo: issue al COO para completar antes de disparar onboarding.

---

## Pasos del workflow

### Paso 1: Parse del SOW
**Output:** estructura JSON con:
- company_name
- primary_contact (name, email, phone, role)
- secondary_contacts (hasta 3)
- scope_summary
- deliverables (lista)
- start_date
- end_date
- total_value
- retainer_value (si aplica)
- billing_cadence (monthly / milestone / etc)
- signature_date
- legal_entity (LLC / S.A. / etc)

---

### Paso 2: Registro en sistemas

**En CRM:**
- Cambiar stage a "implementation".
- Asignar account lead (por default: Javier hasta que escale).
- Poblar todos los fields del SOW.

**En sistema de billing (Stripe / Wise):**
- Crear customer.
- Configurar recurring (si es retainer) o invoice único con pagos escalonados.
- Enviar primera factura según SOW.

**En Paperclip:**
- Crear "Client pod" con sub-issues pre-poblados:
  - Kickoff meeting (deadline: < 5 días).
  - Accesos a sistemas del cliente (deadline: < 7 días).
  - Discovery técnico (deadline: < 10 días).
  - Plan detallado del sprint (deadline: < 14 días).

**En Google Drive / Notion:**
- Clonar `/delivery/client_pods_template/` a `/delivery/clients/{{company_name}}/`.
- Pre-poblar documentos:
  - `00_README.md` (resumen del SOW).
  - `01_business_map.md` (placeholder).
  - `02_task_map.xlsx` (placeholder).
  - `03_roi_calculator.xlsx` (placeholder).
  - `04_opportunity_matrix.md` (placeholder).
  - `05_implementation_scope.md` (placeholder).
  - `06_qa_checklist.md` (placeholder).
  - `07_rollout_plan.md` (placeholder).
  - `99_mbr_log.md` (monthly review log).

---

### Paso 3: Comunicación

**Slack channel compartido:**
- Crear `#client-{{company_slug}}`.
- Invitar: Javier, account lead, cliente primary contact.
- Post de bienvenida con agenda del kickoff.

**Emails de bienvenida:**
- Al cliente: bienvenida + link a agendar kickoff + lista de accesos que vamos a necesitar + link al channel.
- A Javier + account lead: onboarding iniciado, pod creado, próxima acción.

**Calendar:**
- Bloqueo tentativo de kickoff en próximos 5 días hábiles.
- Link de Calendly específico para este cliente.

---

### Paso 4: Discovery técnico preparation

**Checklist de accesos a pedir al cliente:**
(customizable por tipo de proyecto)

- [ ] Read-only access al CRM (HubSpot / Salesforce / Close).
- [ ] Read-only al sistema operativo core (PMS, ERP, LPM, etc).
- [ ] Read access a Slack / Teams (si aplica).
- [ ] Documentos operativos (SOPs, manuales, comunicación de marca).
- [ ] Data muestra anonimizada (1-3 meses).
- [ ] NDA / DPA firmados.
- [ ] Lista de stakeholders + acceso a agenda.

**Formato:** Google Form / Notion page prellenada enviada al cliente en bienvenida.

---

### Paso 5: Kickoff meeting

**Agenda automática (generada por LLM):**
```
1. Bienvenida + presentaciones (5 min)
2. Resumen del SOW y expectativas (10 min)
3. Revisión de outcomes objetivo (10 min)
4. Stakeholders y operadores clave (5 min)
5. Roadmap de los próximos 10 días (15 min)
6. Acceso a sistemas + NDA/DPA (10 min)
7. Cadencia de comunicación y check-ins (5 min)
8. Próximos pasos + quién hace qué (10 min)
```

**Post-kickoff automation (trigger: kickoff meeting terminada):**
- Transcripto Fireflies / Otter guardado al pod.
- LLM genera minuta con acuerdos + next steps.
- Envío de minuta a todos los attendees < 2 h post-meeting.
- Tickets creados en Paperclip según next steps.

---

### Paso 6: Notificaciones al team JM

**A CEO agent:**
- "Cliente {{company_name}} onboardeado. Kickoff agendado para {{date}}. Pod en {{link}}."

**A Head of Audit:**
- "Tu próximo audit: {{company_name}}. Discovery agendado. Prep checklist iniciado."

**A CTO:**
- "Stack técnico a prever: {{resumen del scope técnico}}. Budgets de API estimados: {{USD}}."

**A COO:**
- "Billing configurado. Primera factura enviada. Cadencia: {{mensual / milestone}}."

**A Client Success:**
- "Cliente nuevo. Setup de canal de soporte activado. Retainer inicia día {{X}}."

---

### Paso 7: Dashboard del cliente

- Crear entrada en "Active Clients Dashboard" con:
  - Fecha inicio.
  - Account lead.
  - Retainer tier.
  - Próximo milestone.
  - Próximo MBR.
  - Salud (verde al inicio).

---

## Subflujos por tipo de engagement

### Si es AI Opportunity Audit (10K)
- Discovery técnico condensado en 2 días.
- Audit comienza día 3.
- Timeline de 10 días hábiles.
- Entregable: deck + ROI calculator + business/task map.
- No crear tier de retainer aún.

### Si es Quick Wins Sprint (10-20K)
- Ya viene con audit cerrado. Onboarding = kickoff técnico + accesos.
- Sprint de 4 semanas.
- Daily 9 AM scheduling desde día 1.

### Si es Strategic AI Implementation (25K+)
- Discovery extendido (1 semana).
- Planning sprint separado.
- Crear múltiples workstreams en el pod.
- Fronte-load compliance / legal si hay data sensible.

### Si es AI Operations Retainer (mensual 2-50K)
- Setup de billing recurring.
- Configurar SLA según tier.
- Monthly review cadencia en calendar.
- Health dashboard activo desde día 1.

---

## Error handling

### Qué pasa si:

**Parse del SOW falla** (documento mal formateado):
- Issue al COO para revisar manualmente.
- Workflow pausado con alerta.
- Reintento después de fix.

**Cliente no responde al email de bienvenida en 48 h:**
- Escalation al account lead.
- Segundo email con mención del account lead.
- Si no responde en 72 h: escalation a Javier.

**Kickoff no se agenda en 5 días:**
- Account lead llama directamente al cliente.
- Si no hay progreso en 10 días: escalation al CEO agent.

**Acceso a sistemas bloqueado > 10 días:**
- Issue crítico al CTO + CEO.
- Mail al cliente con urgencia.
- Ajuste de timeline del SOW si corresponde.

---

## Validación post-ejecución

**Checklist automática de completitud (se ejecuta al día 7):**
- [ ] Cliente en CRM con stage correcto.
- [ ] Primera factura enviada y confirmada.
- [ ] Pod creado con todos los documentos placeholder.
- [ ] Slack channel activo con al menos 3 miembros.
- [ ] Kickoff meeting agendado o realizado.
- [ ] Accesos a sistemas entregados o en curso.
- [ ] Todos los agentes relevantes notificados.
- [ ] Dashboard del cliente actualizado.

Si < 80% completado al día 7: alerta al CEO agent + COO.

---

## KPIs del onboarding

| KPI | Target |
|---|---|
| Tiempo SOW firmado → sistemas creados | < 2 h |
| Tiempo SOW firmado → kickoff agendado | < 3 días |
| Tiempo SOW firmado → accesos completos | < 10 días |
| % de clientes con onboarding completo al día 7 | > 90% |
| % de accesos pendientes > 14 días | < 10% |
| Satisfacción del cliente con onboarding (post-survey) | > 4.5/5 |

---

## Customización para vender como CL-004

Cuando un cliente compra este workflow:
1. Adaptar inputs al tipo de cliente (quizá es un onboarding de empleado, no de cliente final).
2. Templates de emails / documentos customizados.
3. Integraciones con sus sistemas (BambooHR, Greenhouse, Salesforce, etc).
4. Signing flow adaptado (su DocuSign tenant).
5. Dashboard con su branding.

**Pricing**: 15-30K implementación + 1-2K/mes retainer.

---

## Ver también

- `/n8n/workflow-inventory.md` (JM-03 y CL-004)
- `/delivery/quick-wins-sprint.md`
- `/delivery/handoff-template.md`
- `/paperclip/coo-instructions.md`
