# Skills — JM Consulting OS

Cada carpeta es una skill que se carga en Paperclip. Las skills están separadas por agente + una skill compartida (`jm-knowledge`) que todos cargan.

## Estructura

```
skills/
├── jm-knowledge/     ← Shared: todos los agentes la cargan
├── ceo/              ← CEO (Alex) — decisiones, cadencia semanal
├── cro/              ← CRO (Sol) — ventas, outbound, calificación
├── head-of-audit/    ← Andrés — metodología audit, deliverables
├── cto/              ← Tomás — sprints, stack, incidentes
├── coo/              ← Clara — operaciones, facturación, SOPs
└── cmo/              ← Mei — contenido, LinkedIn, marca
```

## Cómo agregar una skill a un agente en Paperclip

1. Ir al agente → tab **Skills**.
2. Hacer click en **"View company skills library"**.
3. Activar el checkbox de la skill correspondiente.
4. La skill se materializa en el próximo run del agente.

## Skills por agente

| Agente | Skills a activar |
|---|---|
| CEO (Alex) | `jm-knowledge` + `ceo` |
| CRO (Sol) | `jm-knowledge` + `cro` |
| Head of Audit (Andrés) | `jm-knowledge` + `head-of-audit` |
| CTO (Tomás) | `jm-knowledge` + `cto` |
| COO (Clara) | `jm-knowledge` + `coo` |
| CMO (Mei) | `jm-knowledge` + `cmo` |

## Qué contiene cada skill

### jm-knowledge (compartida — todos)
- mission_vision.md
- core_values.md
- org_chart.md
- pricing_service_ladder.md
- heartbeat-policy.md
- approvals-policy.md
- glossary.md
- client_conduct.md

### ceo
- soul.md — identidad, principios, tono, qué nunca hace
- decision-matrix.md — qué decide solo vs. escala a Javier
- weekly-cadence.md — cadencia semanal, dispatch, cliente en riesgo

### cro
- soul.md — identidad, reglas de email, escalaciones
- qualification-framework.md — ICP, scoring, stage definitions
- outbound-rules.md — estructura de email, cadencia, KPIs
- objection-handling.md — 7 objeciones top con respuestas
- discovery-call-guide.md — Yesterday Morning Method en ventas

### head-of-audit
- soul.md — identidad, principios, deliverables, escalaciones
- audit-methodology.md — proceso completo de 10 días
- yesterday-morning-method.md — técnica de entrevista
- deliverables-checklist.md — checklist de calidad por deliverable

### cto
- soul.md — identidad, stack preferido, principios técnicos
- sprint-framework.md — 4 semanas, canary, signoff, KPIs
- incident-response.md — Sev 1/2/3, SLA, post-mortem

### coo
- soul.md — identidad, dominios, KPIs
- billing-sops.md — ciclo mensual, recordatorios, onboarding cliente

### cmo
- soul.md — identidad, voz de marca, principios de contenido
- linkedin-playbook.md — estructura de post, hooks, calendario
- content-checklist.md — checklist de calidad antes de publicar
