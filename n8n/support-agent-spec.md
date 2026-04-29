# Support Agent Spec — Agente de soporte para clientes

Spec del agente que se instala en cliente para triage, respuesta y handoff de tickets / consultas.

## Overview

"Support Agent" es uno de los workflows insignia de JM (CL-003 en el inventory). Se customiza por cliente y vertical. Resuelve 40-60% de consultas sin humano, escala el resto con contexto completo.

---

## Para quién
- **Property management**: consultas de inquilinos (mantenimiento, pagos, leasing info).
- **Accounting firms**: consultas de clientes sobre status de libros, deadlines, requests de info.
- **Legal boutiques**: preguntas de clientes sobre status de casos, documentos, próximos pasos.
- **SaaS teams**: tickets técnicos y de uso de producto.

---

## Arquitectura

```
┌──────────────────────────────────────────────┐
│   Canales de entrada                         │
│   - Email (webhook / inbox monitoring)       │
│   - Chat widget (Intercom / HubSpot chat)    │
│   - WhatsApp (Twilio / Meta API)             │
│   - Formulario web                           │
└───────────────────┬──────────────────────────┘
                    │
                    ▼
┌──────────────────────────────────────────────┐
│   1. Ingesta + normalización                 │
│   - Unifica formato a un schema interno      │
│   - Extrae: sender, subject, body, metadata  │
└───────────────────┬──────────────────────────┘
                    │
                    ▼
┌──────────────────────────────────────────────┐
│   2. Enriquecimiento de contexto             │
│   - Look-up del sender en CRM / DB           │
│   - Historial de interacciones previas       │
│   - Status de cuenta / caso / contrato       │
└───────────────────┬──────────────────────────┘
                    │
                    ▼
┌──────────────────────────────────────────────┐
│   3. Classifier (Claude)                     │
│   - Intent: info / action / complaint / sales│
│   - Sev: 1-4                                 │
│   - Topic: billing / technical / etc.        │
│   - Auto-resolve possible: yes/no            │
└───────────┬────────────────────┬─────────────┘
            │                    │
     auto-resolve         escalate to human
            │                    │
            ▼                    ▼
┌─────────────────────┐  ┌─────────────────────┐
│  4. Response agent  │  │  5. Routing agent   │
│  (RAG over KB)      │  │  - Routea por topic │
│  - Redacta respuesta│  │  - Notifica operador│
│  - Valida con reglas│  │  - Draft a humano   │
│  - Envía si confianza│ │  - Tracking de SLA  │
│    > umbral         │  └─────────────────────┘
└─────────────────────┘
            │
            ▼
┌──────────────────────────────────────────────┐
│   6. Log + analytics                         │
│   - Status del ticket                        │
│   - Tiempo de resolución                     │
│   - Auto-resolve rate                        │
│   - Satisfacción (feedback loop)             │
└──────────────────────────────────────────────┘
```

---

## Componentes técnicos

### Vector DB de knowledge base
- Supabase pgvector / Pinecone / Weaviate.
- Chunks de: documentos del cliente, FAQs, procedimientos, términos.
- Embeddings con OpenAI `text-embedding-3-large` o Claude-compatible.
- Refresh automático semanal si hay docs nuevos.

### Classifier
- Claude (Sonnet para clasificación + Haiku para tasks de bajo costo).
- Prompt con few-shot por cliente.
- Output estructurado JSON.

### Response generator
- Claude (Sonnet o Opus según complejidad).
- RAG: top-3 chunks + contexto de la cuenta.
- Reglas hardcoded para casos sensibles:
  - Si menciona "cancelación" / "refund" → nunca auto-resolve.
  - Si menciona "legal" / "sue" / "attorney" → escalation inmediata.
  - Si tema financiero > 500 USD → escalation.

### Humano-in-the-loop (primer mes)
- 100% de respuestas pasan por operador antes de enviar (primer mes).
- A partir del mes 2: solo respuestas con confianza < 85% pasan por operador.
- Mes 3+: muestras aleatorias 10% para QA continuous.

### SLA tracking
- Timer por ticket desde ingesta.
- Alertas si supera umbral (default: Sev 1 = 1 h, Sev 2 = 4 h, Sev 3 = 24 h, Sev 4 = 72 h).

---

## Prompt base del classifier

```
Sos un clasificador de tickets para {{company_name}}, una empresa de {{vertical}}.

Tu tarea: clasificar el ticket en las siguientes dimensiones.

1. Intent:
   - info_request (pide información)
   - action_request (pide que hagamos algo)
   - complaint (se queja de algo)
   - sales_inquiry (pregunta por servicios)
   - other

2. Severity:
   - 1 (crítico - downtime, legal, seguridad)
   - 2 (urgente - impacta operación)
   - 3 (normal)
   - 4 (bajo - info general)

3. Topic:
   - {{lista customizada por cliente}}

4. Auto-resolve possible (true/false):
   - Solo true si:
     - Tema está cubierto en knowledge base.
     - Pregunta es clara y específica.
     - No involucra cambios de datos, refunds, o decisiones de política.

5. Extract:
   - sender_identifier (email, phone, account_id).
   - key_entities (contract #, property #, case #).
   - sentiment (positive, neutral, negative, angry).

Output: JSON con todos los campos.
```

---

## Prompt base del response generator

```
Sos el agente de soporte de {{company_name}}.

Contexto del cliente (sender):
{{cuenta_info}}

Historial reciente:
{{últimas 3 interacciones}}

Ticket actual:
{{ticket_body}}

Información relevante de nuestra knowledge base:
{{top_3_chunks}}

Instrucciones:
1. Responde en tono {{tono_cliente}} (formal / casual / etc).
2. Idioma: {{idioma}}.
3. Extensión: 80-150 palabras.
4. Si NO encontrás respuesta clara en la KB: escribí "ESCALATE" y explicá brevemente por qué.
5. Si respondés: terminá con una pregunta abierta de confirmación ("¿Esto responde tu consulta?").
6. NUNCA inventes números, fechas, precios o términos legales. Si no están en la KB, escalate.
7. NUNCA hagas promesas de timeline si no están validadas.
```

---

## Datos que maneja

### Input mínimo (por cliente)
- Lista de channels activos con credenciales.
- Knowledge base de documentos (mínimo 20-50 docs iniciales).
- Acceso a CRM / DB para look-up de cuenta (read-only).
- Lista de topics y tono de voz.
- Reglas hardcoded de escalation.

### Output
- Respuesta al canal original.
- Ticket tracking en sistema de destino (Zendesk, HubSpot, custom).
- Log completo de cada interacción.
- Dashboard con métricas.

---

## KPIs por cliente

| KPI | Target fase 1 (mes 1-3) | Target fase 2 (mes 3+) |
|---|---|---|
| Auto-resolve rate | 20-30% | 40-60% |
| Accuracy (validada humano) | > 90% | > 95% |
| Tiempo primera respuesta | < 5 min | < 2 min |
| Escalation correcta | > 85% | > 95% |
| Satisfacción (thumbs up / rate) | > 4/5 | > 4.5/5 |
| Costo por ticket | < 0.10 USD | < 0.05 USD |
| Incidentes Sev 1 detectados por agente | 100% | 100% |

---

## Setup process (por cliente)

### Semana 1
- Kickoff técnico: credenciales, integraciones, acceso a data.
- Carga de KB inicial.
- Configuración de classifier con taxonomía del cliente.

### Semana 2
- Primer prototipo funcionando con data real.
- Test con 20-30 tickets históricos.
- Ajuste de prompts.

### Semana 3 (canary)
- Live con 10-20% de tráfico.
- 100% de respuestas revisadas por operador antes de enviar.
- Iteración diaria del prompt.

### Semana 4 (full)
- 100% de tráfico.
- Empieza auto-send para confianza > 85%.
- Dashboard operativo + runbook.

### Post-mes 1 (retainer)
- Monthly review: accuracy, auto-resolve, satisfacción, nuevos topics.
- Refinement continuo.

---

## Guardrails críticos

### Nunca auto-responder si:
- Intent = complaint con sentiment = angry.
- Menciona: cancelación, refund, legal, abogado, lawsuit, seguridad, datos personales.
- Monto involucrado > umbral configurado.
- Sender es VIP (flag en CRM).
- Respuesta involucra tomar una acción irreversible.

### Nunca generar/modificar data productiva:
- El agente responde y enruta.
- Acciones de modificación (ej: actualizar fecha, cambiar plan) las hace un humano o un workflow separado con approval.

### Auditoría
- 100% de mensajes enviados quedan loggeados.
- Revisión semanal por operador cliente (sampling de 5-10%).
- Red team del CTO JM cada trimestre.

---

## Integración con otros workflows

### Upstream
- CL-004 (onboarding): carga la cuenta en el CRM + knowledge base.
- CL-010 (dashboard): consume métricas del support agent.

### Downstream
- CL-009 (health monitor): usa señales de tickets para score de salud.
- JM-04 (maintenance reporting): incluye métricas en MBR.

---

## Costos estimados (cliente mediano, 500-1000 tickets/mes)

| Componente | Costo mensual |
|---|---|
| Claude API (classifier + responder) | 80-200 USD |
| Embeddings + vector DB | 30-80 USD |
| n8n / infra | 50-100 USD |
| Observability (Langfuse) | 50-100 USD |
| **Total** | **~210-480 USD/mes** |

Comparativo: 1 agente humano full-time manejaría este volumen por 2.500-5.000 USD/mes.
ROI del cliente: 5-15x.

---

## Anti-patterns

- Saltar humano-in-the-loop los primeros 30 días.
- KB desactualizada → el agente responde con info vieja.
- Responder todos los tickets auto (incluso los que deberían escalarse).
- Clasificador sin metrics de accuracy trackeado.
- No separar environments (dev, staging, prod).
- Rollout 100% sin canary.

---

## Ver también

- `/n8n/workflow-inventory.md` (CL-003)
- `/delivery/quick-wins-sprint.md`
- `/delivery/qa-checklist.md`
- `/maintenance/retainer-model.md`
