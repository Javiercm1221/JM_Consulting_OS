# Sales Engine Spec — Motor de outbound de JM

Spec completa del sales engine interno de JM Consulting: stack, workflows, datos y KPIs.

## Overview

El sales engine de JM combina 4 capas:
1. **Intel** — enriquecimiento de prospectos (Apify, Vibe Prospecting, Apollo, Clay).
2. **Outreach** — envío multi-canal (Instantly email, HeyReach LinkedIn).
3. **CRM** — tracking del pipeline (Close / HubSpot / Airtable).
4. **Agent layer** — CRO agent coordina, decide, genera copy, responde.

---

## Stack

### Fuente de prospectos
- **Apify** — scraping de directorios sectoriales (property mgmt, accounting, legal).
- **Apollo** — base B2B con filtros de industria, geo, tamaño, role.
- **LinkedIn Sales Navigator** — búsqueda de decision-makers con señales de intent.
- **Clay** — orquestación y enriquecimiento multi-fuente.
- **Vibe Prospecting** — búsqueda y enriquecimiento con data fresca.

### Enriquecimiento
- **Email verification** (NeverBounce, ZeroBounce o similar).
- **LinkedIn scraping** (headline, company, tenure).
- **Firmographics** (tamaño, revenue estimado, tech stack).
- **Intent signals** (hiring, funding, noticias recientes).

### Outreach
- **Instantly** — email outbound con multi-inbox warmup.
- **HeyReach** — LinkedIn outreach automatizado.
- **Gmail / Resend** — respuestas 1:1 post-reply.

### CRM
- **Close** (recomendado para SaaS-style pipeline) o **HubSpot Free** o **Airtable custom**.
- Stages: `lead → contacted → replied → qualified → discovery scheduled → discovery done → audit proposed → audit closed → implementation`.

### Observabilidad
- Dashboard en Metabase / Retool / Airtable views.
- Métricas diarias exportadas a Notion.

---

## Arquitectura del workflow

```
┌─────────────────────────────────────────────┐
│  1. Fuente de prospectos (Apollo / Apify)   │
└──────────────┬──────────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────────┐
│  2. Clay orquesta enriquecimiento           │
│     (email verify, LinkedIn, firmographics) │
└──────────────┬──────────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────────┐
│  3. CRO agent (Claude)                      │
│     - Valida fit con ICP                    │
│     - Personaliza copy por vertical         │
│     - Decide canal y cadencia               │
└──────────────┬──────────────────────────────┘
               │
        ┌──────┴──────┐
        ▼             ▼
┌─────────────┐  ┌─────────────┐
│  Instantly  │  │  HeyReach   │
│  (email)    │  │  (LinkedIn) │
└──────┬──────┘  └──────┬──────┘
       │                │
       └──────┬─────────┘
              │
              ▼
┌─────────────────────────────────────────────┐
│  4. Reply detector (JM-01 workflow)         │
│     - Clasifica interés                     │
│     - Actualiza CRM                         │
│     - Notifica CRO agent                    │
└──────────────┬──────────────────────────────┘
               │
               ▼
┌─────────────────────────────────────────────┐
│  5. CRO agent responde + agenda discovery   │
└─────────────────────────────────────────────┘
```

---

## Especificación de cada workflow

### SE-01: Prospect sourcing
**Frecuencia:** semanal, lunes 7 AM.
**Pasos:**
1. Trigger cron.
2. Ejecuta búsqueda en Apollo con filtros guardados (vertical del sprint).
3. Ejecuta scraping en Apify de directorios sectoriales nuevos.
4. Merge + dedup contra CRM existente.
5. Push a tabla "Prospects - Raw" en Airtable.
6. Notifica al CRO agent con count y preview.

**Target:** 200-400 prospectos nuevos/semana.

---

### SE-02: Enrichment pipeline
**Frecuencia:** diaria, procesa batch de Raw.
**Pasos:**
1. Pull prospectos en "Raw" sin enriquecer.
2. Clay:
   - Verifica email.
   - Scrape LinkedIn.
   - Firmographics.
   - Intent signals (news, funding).
3. Score de fit (LLM + reglas ICP).
4. Si score > 60: mover a "Ready to outreach".
5. Si score 40-60: mover a "Nurture".
6. Si score < 40: marcar "Not fit" + razón.

**Target:** 70%+ de enrichment exitoso, 50%+ Ready-to-outreach.

---

### SE-03: Campaign launch
**Frecuencia:** cada vez que el CRO lanza un nuevo batch.
**Pasos:**
1. CRO selecciona batch de "Ready to outreach" (50-100 prospectos).
2. CRO elige campaña (PM-E1, PM-E2, Acc-E1, etc. de `/sales/campaign-templates.md`).
3. LLM personaliza campos dinámicos por prospecto:
   - Hook con dato de la empresa.
   - Stat específico del vertical.
   - Name / company / role.
4. Push a Instantly (cadencia 4 toques en 14 días).
5. Push a HeyReach si LinkedIn cadencia activa.
6. Log en CRM con campaña asignada.
7. Notifica al CRO para monitor.

**Target:** 2.500-3.500 emails/mes, 500-800 LinkedIn touches/mes.

---

### SE-04: Reply detection + classification (JM-01 expandido)
**Frecuencia:** event-driven.
**Pasos:**
1. Webhook de Instantly cuando hay reply.
2. LLM classifier:
   - Positivo (interesado / quiere meeting).
   - Cauto (pide info, no rechaza).
   - Objeción específica (budget, timing, scope).
   - Rechazo explícito.
   - Out-of-office.
   - Fuera de scope (wrong person).
3. Actualiza stage en CRM.
4. Genera draft de respuesta personalizada.
5. Alerta al CRO con prioridad según categoría.
6. Si "positivo": auto-agenda discovery slot sugerido.

**Target:** clasificación correcta > 85%, tiempo reply-to-first-response < 2 h.

---

### SE-05: Discovery prep
**Frecuencia:** event-driven, 24 h antes de cada discovery call.
**Pasos:**
1. Trigger 24 h antes del meeting.
2. Pull data del prospecto (CRM + LinkedIn + website + noticias recientes).
3. LLM genera brief:
   - Contexto de la empresa.
   - Role del attendee.
   - Posibles puntos de dolor por vertical.
   - Hipótesis de fit.
   - 5 preguntas clave a hacer en la call.
4. Envía brief al CRO + Javier.
5. Agenda follow-up post-call.

**Target:** briefs disponibles 24 h antes en 100% de calls.

---

### SE-06: Post-discovery follow-up
**Frecuencia:** event-driven, post-call.
**Pasos:**
1. Transcript de Fireflies / Otter.
2. LLM genera:
   - Summary estructurado (dolor, budget, timing, stakeholders, next steps).
   - Draft de email follow-up.
   - Evaluación de fit y probabilidad de cerrar.
3. Actualiza CRM stage.
4. Si fit: genera draft de propuesta de audit.
5. Si no-fit: mueve a "archived" + razón + eventual re-engage en 6 meses.

**Target:** follow-up enviado < 24 h post-call en 95% de casos.

---

## Datos y estructura

### Tablas principales (en Airtable o CRM)

**Prospects**
- id, email, first_name, last_name, title, linkedin_url, company_name, company_url, industry, vertical_jm (pm/acc/legal/etc), company_size, geo_city, geo_state, fit_score, source, status, created_at, last_contacted_at.

**Campaigns**
- id, code (PM-E1), vertical, cadence, created_by, status, start_date, end_date.

**Touches**
- id, prospect_id, campaign_id, channel (email/linkedin), step, sent_at, opened_at, replied_at, reply_classification, response_draft.

**Deals**
- id, prospect_id, stage, audit_value, implementation_value, retainer_value, close_probability, expected_close_date, actual_close_date, owner.

---

## KPIs del sales engine

| KPI | Target | Medición |
|---|---|---|
| Prospectos enriquecidos/mes | 2.000+ | SE-02 output |
| Emails enviados/mes | 2.500-3.500 | SE-03 |
| LinkedIn touches/mes | 500-800 | SE-03 |
| Open rate | > 50% | Instantly |
| Reply rate total | 5-10% | Instantly + LinkedIn |
| Reply rate positivo | 1.5-3% | SE-04 |
| Discovery calls/mes | 15-30 | Calendly |
| Show rate | > 75% | Calendly vs actual |
| Discovery → Audit propuesto | > 40% | CRM |
| Audit propuesto → cerrado | > 50% | CRM |
| Audits cerrados/mes | 2-4 | CRM |
| Costo por audit cerrado | < 1.000 USD | Cost por mes / audits cerrados |

---

## Costos estimados del sales engine

| Herramienta | Costo mensual |
|---|---|
| Apollo | 49-99 USD |
| Apify | 49-100 USD (usage based) |
| Clay | 149-349 USD |
| Instantly | 37-97 USD (+$/inbox extra) |
| HeyReach | 79-199 USD |
| Dominios secundarios | 10-30 USD |
| Email warmup | incluido o 50 USD |
| CRM (Close / HubSpot) | 0-99 USD |
| Email verification | 20-50 USD |
| **Total** | **~400-900 USD/mes** |

Con esto: sales engine costea < 2% de revenue cuando la firma factura 40-60K/mes.

---

## Playbook de escalamiento

### Mes 1 (setup)
- 1 dominio + 2 inboxes + 1.000-1.500 emails/mes.
- Foco: 1 vertical (property mgmt).
- Meta: 1-2 audits cerrados.

### Mes 2-3
- 3 dominios + 6 inboxes + 3.000-4.000 emails/mes.
- 2 verticales.
- Meta: 3-5 audits cerrados, 1-2 retainers firmados.

### Mes 4-6
- 5 dominios + 10 inboxes + 5.000-8.000 emails/mes.
- 3-4 verticales.
- Meta: 6-10 audits cerrados, 3-5 retainers activos.

### Mes 7-12
- 8+ dominios + 16+ inboxes + 12.000-16.000 emails/mes.
- Todas las verticales activas.
- Meta: pipeline suficiente para cerrar 2-4 implementaciones/mes + retainers.

---

## Anti-patterns del sales engine

- Usar 1 solo dominio para alto volumen (se quema).
- No rotar copy (quema domains y prospectos).
- Outreach sin enriquecimiento (tasa de reply < 2%).
- Respuestas automáticas genéricas post-reply (rompe la señal humana).
- No trackear stages en CRM (pipeline ciego).
- Escalar volumen antes de validar copy ganador.
- Reutilizar prospectos quemados sin refrescar (bajo ROI).

---

## Ver también

- `/sales/outbound-playbooks.md`
- `/sales/campaign-templates.md`
- `/sales/niches.md`
- `/sales/icps.md`
- `/n8n/workflow-inventory.md`
- `/paperclip/cro-instructions.md`
