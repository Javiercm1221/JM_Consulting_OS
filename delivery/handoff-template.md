# Handoff del Audit a Delivery

Proceso formal para pasar del audit firmado a la implementación. Sin handoff estructurado, el proyecto se diluye en las 2 primeras semanas.

## Cuándo se ejecuta

Una vez que el cliente firma el SOW de implementación (Opción A, B o C del deck).

## Duración

1 día calendario. Máximo 48 h desde firma del SOW.

---

## Entregables del handoff

### Del equipo Audit al equipo Delivery

1. **Business map v1** — PNG + MD (validado).
2. **Task map v1** — XLSX (validado).
3. **Opportunity matrix** — XLSX + PNG.
4. **ROI Calculator** — XLSX.
5. **Transcripts de entrevistas** — MD, una por persona.
6. **Outcomes firmados** — PDF + MD.
7. **Audit Deck** — PPTX + PDF.
8. **SOW firmado** — PDF.
9. **Client pod en Paperclip** — link al workspace del cliente.
10. **CRM stage actualizado** — "Audit closed → Delivery kickoff".

### Del equipo Delivery al cliente (al final del handoff)

1. **Kickoff email** — con agenda y documentos adjuntos.
2. **Calendar invite de kickoff** — 90 min.
3. **Shared workspace** — acceso a Paperclip / Notion / compartido.
4. **Slack canal compartido** (si aplica).
5. **Responsable JM único** — point of contact designado.

---

## Checklist del handoff (1 página, ejecutable)

```
# Handoff — {{Company}} — {{date}}

## Pre-requisitos
- [ ] SOW firmado por sponsor ejecutivo.
- [ ] Deposit recibido (50% del Q1 típicamente).
- [ ] PO creada (si aplica en el cliente).

## Transferencia de activos
- [ ] Business map copiado a /delivery/clients/{{company}}/
- [ ] Task map copiado idem.
- [ ] ROI Calculator copiado.
- [ ] Transcripts copiados y anonimizados.
- [ ] Audit Deck archivado.
- [ ] Outcomes firmados archivados.

## Setup técnico
- [ ] Client pod creado en Paperclip.
- [ ] Agente de Delivery PM asignado (ver `/paperclip/agents/`).
- [ ] Canal Slack creado (si cliente lo quiere).
- [ ] Repositorio Git privado creado (si hay código).
- [ ] Credenciales/secrets vault creado (1Password / Bitwarden).
- [ ] Accesos a sistemas del cliente solicitados y recibidos.

## Reunión interna JM
- [ ] Team briefing: 30 min con quien hizo el audit + quien hará delivery.
- [ ] Walk-through del Opportunity Matrix.
- [ ] Decisión de orden de quick wins (Q1 arranque).
- [ ] Riesgos transferidos por escrito.
- [ ] Contact principal del cliente identificado.

## Reunión con cliente
- [ ] Kickoff agendado (90 min en las 2 próximas semanas).
- [ ] Agenda del kickoff enviada.
- [ ] Stakeholders confirmados.
```

---

## Estructura del client pod en Paperclip

Cada cliente tiene su workspace (issue tracker).

```
/delivery/clients/{{company}}/
  ├── README.md               ← contexto + outcomes + sponsor
  ├── outcomes-signed.pdf
  ├── business-map.md + .png
  ├── task-map.xlsx
  ├── opportunity-matrix.xlsx + .png
  ├── roi-calculator.xlsx
  ├── audit-deck.pptx + .pdf
  ├── sow-signed.pdf
  ├── interviews/
  │   ├── {{name}}-{{role}}.md
  │   └── ...
  ├── workstreams/
  │   ├── quickwin-1-lead-response/
  │   │   ├── scope.md
  │   │   ├── spec.md
  │   │   ├── progress.md
  │   │   └── assets/
  │   ├── quickwin-2-ticket-classification/
  │   └── ...
  ├── status/
  │   ├── 2026-01-week-01.md
  │   ├── 2026-01-week-02.md
  │   └── ...
  └── handoff-to-maintenance.md  ← se completa al cierre del proyecto
```

---

## Kickoff agenda (90 min)

### Objetivo
Alinear equipo y calendario, remover ambigüedad.

### Estructura

**Bloque 1 — Bienvenida (5 min)**
- Presentación equipo JM asignado.
- Presentación equipo cliente asignado.

**Bloque 2 — Recap del audit (15 min)**
- Resumen de outcomes.
- Top 3 oportunidades seleccionadas.
- ROI esperado.

**Bloque 3 — Plan de trabajo (30 min)**
- Roadmap 90 días.
- Semana a semana.
- Owners por workstream.
- Dependencias del cliente (data, accesos, decisiones).

**Bloque 4 — Operativa (20 min)**
- Cadencia: weekly stand-up de 30 min (día / hora fija).
- Monthly: revisión de métricas (90 min con sponsor).
- Canal de comunicación: Slack / email.
- Escalación: ruta clara si algo se traba.

**Bloque 5 — Riesgos y supuestos (15 min)**
- Top 5 riesgos con mitigación.
- Supuestos críticos (data, talento, compliance).
- Criterios de "parar todo y replantear".

**Bloque 6 — Next steps (5 min)**
- Fecha de próxima standup.
- Accesos pendientes del cliente.
- Deliverable de la semana 1.

### Grabar la sesión
- Subir a `/delivery/clients/{{company}}/status/kickoff-recording.mp4`.
- Transcripción automática cargada a Paperclip.

---

## Reglas innegociables

1. **No arrancar trabajo técnico sin kickoff hecho.**
2. **Un solo point of contact del lado JM.** Si el cliente escribe a 3 personas, todas rebotan al PM asignado.
3. **Accesos en < 7 días.** Si el cliente no entrega accesos en 7 días, se pausa el cronograma sin costo JM (descuento en penalidad).
4. **Weekly status por escrito.** Aunque haya standup verbal, lunes por la mañana hay un MD con status de la semana anterior.
5. **Cambios de scope → change order.** Si el cliente pide algo fuera del SOW, se emite un CO formal antes de ejecutar.

---

## Métricas del proceso de handoff (para mejora continua)

- Tiempo desde firma del SOW hasta kickoff: target < 14 días.
- Accesos recibidos dentro de 7 días del kickoff: target > 90%.
- Deliverable semana 1 entregado: target 100%.
- Sponsor satisfaction post-kickoff (encuesta 1 pregunta): target > 8/10.

---

## Ver también

- `/delivery/implementation-scope.md` — cómo se define el scope
- `/delivery/quick-wins-sprint.md` — estructura del primer sprint
- `/delivery/rollout-plan.md` — plan de rollout general
- `/delivery/change-management.md` — gestión del cambio humano
