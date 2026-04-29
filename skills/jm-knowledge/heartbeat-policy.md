# Heartbeat Policy — Cuándo se activa cada agente

Define cuándo cada agente de JM Consulting "se despierta" en Paperclip: ritmo fijo, eventos disparadores, guardias, estados idle.

## Principio base

No queremos agentes que corran 24/7 sin motivo (costo + ruido), ni agentes que duerman cuando pasan cosas (pérdida de oportunidad). El heartbeat es el contrato de cuándo se activa cada uno.

Tres modos de activación:
- **Rhythmic (calendario)**: se activa en horarios fijos.
- **Event-driven**: se activa cuando pasa algo específico (nuevo lead, issue asignado, incidente).
- **On-call / guardia**: disponible en ventana horaria para responder rápido a ciertos eventos.

---

## Tabla maestra de heartbeat

| Agente | Modo principal | Ventana activa | Eventos disparadores |
|---|---|---|---|
| **CEO** | Rhythmic | Lun 9 AM + Vie 17 PM | Escalation Sev 1, request de Javier, weekly close |
| **CRO** | Rhythmic + event | L-V 9 AM - 18 PM | Reply en Instantly, discovery agendado, CRM stage change |
| **Head of Audit** | Event-driven | Cuando hay audit activo | Kickoff agendado, handoff de CRO, milestone del audit |
| **CTO** | Event + on-call | Durante sprint: L-V 9-18 + guardia off-hours | Sprint activo, incidente Sev 1-2, PR review |
| **COO** | Rhythmic | Lun 8 AM, Vie 17 PM, día 1/3/15/25 de mes | Invoice vencido, contrato para firmar, gasto nuevo |
| **CMO** | Rhythmic light | Lun 9 AM (planning) + 2 ventanas/sem de draft | Case study aprobado, lanzamiento del mercado |
| **Client Success** | Rhythmic + on-call | L-V 9 AM - 18 PM + guardia por SLA | Ticket de cliente, retainer renewal, MBR agendada |

---

## Detalle por agente

### CEO

**Rhythmic:**
- **Lunes 9:00 AM** — Weekly kickoff. Lee status de los 6 subordinados, define prioridades de la semana, asigna issues bloqueantes.
- **Viernes 17:00 PM** — Weekly close. Lee reportes viernes de cada agente, genera resumen ejecutivo, marca wins/misses, planifica próxima semana.

**Event-driven:**
- Incidente Sev 1 en cualquier cliente.
- Request directo de Javier (mención en issue o mensaje).
- Retainer lost o cliente en riesgo.
- Oportunidad > 25K USD.

**Idle:** martes a jueves, salvo que haya disparador.

**Budget de tokens/día:** bajo. No corre continuous.

---

### CRO (Chief Revenue Officer)

**Rhythmic:**
- **L-V 9:00 AM** — Inbox check: replies de Instantly, LinkedIn, CRM.
- **L-V 10:00 AM** — Follow-ups pendientes.
- **L-V 14:00 PM** — Discovery calls o post-call actions.
- **L-V 17:00 PM** — Wrap-up, CRM hygiene, log del día.
- **Viernes 17:00 PM** — Weekly report al CEO.

**Event-driven:**
- Reply positivo en Instantly → calificar + responder en < 2 h.
- Discovery call agendada → prep (account research).
- Lead calificado → mover stage en CRM.
- Lead stale > 7 días → auto-nudge o cierre.

**Ventana horaria:** L-V 9-18 US Eastern (o ajustado por timezone target).

**Budget de tokens/día:** medio-alto durante campaigns activas.

---

### Head of AI Audit

**Event-driven principal:**
- Handoff de CRO (audit vendido) → kickoff scheduling.
- Milestone del audit (día 1, 3, 5, 7, 10) → siguiente paso.
- Pregunta del cliente durante audit.
- Handoff a CTO (post-audit).

**Rhythmic dentro de audit activo:**
- Daily 9 AM durante los 10 días del audit.
- Check-in con operadores cliente cada 48 h.

**Idle:** cuando no hay audit activo. Usa ese tiempo para refinar templates y knowledge base.

**Budget de tokens/día:** alto durante audit (workload concentrado 10 días).

---

### CTO

**Durante sprint activo (4 semanas):**
- **Daily 9:00 AM** — Stand-up: status, bloqueos, plan del día.
- **Daily 17:00 PM** — EOD wrap: commits, métricas, update a cliente.
- **On-call todo el día** — responde a incidentes en < 30 min MTTA.
- **Off-hours** — alerta sólo si Sev 1.

**Entre sprints:**
- **Miércoles 15:00 PM** — Review semanal de dashboards de clientes en retainer.
- Event-driven sólo.

**Event-driven:**
- Incidente Sev 1 o Sev 2 en cualquier cliente.
- PR review request.
- Issue asignado por CEO / Head of Audit / Javier.
- Alerta de costo API > 120% budget.

**Budget de tokens/día:** muy alto durante sprints, bajo entre sprints.

---

### COO

**Rhythmic mensual:**
- **Día 1** — Generar facturas de retainers activos.
- **Día 2** — Facturas de milestones cerrados.
- **Día 3** — Enviar facturas + generar P&L del mes anterior.
- **Día 15** — Recordatorios de facturas no pagadas.
- **Día 25** — Escalation de impagos.

**Rhythmic semanal:**
- **Lunes 8 AM** — Inbox + plan semanal + revisión de tracker financiero.
- **Viernes 17 PM** — Weekly close + report al CEO.

**Event-driven:**
- Invoice a pagar recibido.
- Contrato a firmar.
- Gasto nuevo > 500 USD (aviso al CEO si > 1K).
- Tool down > 2 h.
- Cliente comunica issue de billing.

**Budget de tokens/día:** bajo-medio. Picos los días 1-3 y 15-25.

---

### CMO

**Rhythmic:**
- **Lunes 9:00 AM** — Planning semanal + scheduling de contenido.
- **Martes 10:00 AM** — Draft de newsletter + 1 post LinkedIn.
- **Jueves 10:00 AM** — Draft de 2 posts LinkedIn + review de analytics.

**Event-driven:**
- Case study aprobado → draft de post/newsletter.
- Lanzamiento de modelo / herramienta del mercado (si aplica a vertical).
- Request del CEO / Javier.
- Crítica pública o oportunidad de respuesta.

**Idle:** martes tarde, miércoles, jueves tarde, viernes, fines de semana.

**Budget de tokens/día:** bajo. Contenido batched.

---

### Client Success

**Rhythmic:**
- **L-V 9:00 AM** — Check de tickets abiertos + bandeja de entrada de clientes.
- **L-V 17:00 PM** — Update al CTO / Head of Audit si hay escalation pendiente.
- **Primer miércoles del mes** — Monthly Business Review de cada cliente activo.
- **Viernes 17 PM** — Weekly report de salud de cuenta al CEO.

**On-call:**
- Durante horas laborales del cliente.
- SLA response < 4 h para tier 2+, < 1 h para tier 3+.

**Event-driven:**
- Ticket nuevo del cliente.
- Métrica del cliente fuera de rango (alert del dashboard).
- Retainer renewal en < 30 días.
- NPS / satisfaction negativo.

**Budget de tokens/día:** medio. Aumenta cuantos más clientes activos.

---

## Horarios globales de JM Consulting

Timezone de referencia: **America / New_York** (US Eastern).

Si el cliente está en otro timezone (ej: LA, LATAM), cada agente ajusta la ventana laboral al cliente, no al agente.

Ventana global activa: **Lunes a Viernes 8:00 AM - 19:00 PM ET**.
- Weekend: solo guardia para Sev 1 en retainers activos.
- Nights (19 PM - 8 AM): alertas automáticas sólo, no trabajo proactivo.

---

## Overrides y excepciones

### "Firefighting mode"
Cuando hay un incidente Sev 1 en producción:
- CTO y Client Success se activan inmediatamente (independiente de ventana).
- CEO es notificado.
- COO ajusta comunicación al cliente si corresponde.
- Todos los otros agentes pausan sus tareas no urgentes hasta que se resuelva.

### "Closing mode"
Última semana del trimestre:
- CRO en modo sync continuous.
- COO se activa todos los días.
- CEO review diario.

### "Quiet mode"
Fines de semana + feriados US:
- Solo CTO on-call para Sev 1.
- Resto de agentes apagados.
- Javier puede pedir activación manual si necesita.

---

## Monitoreo del heartbeat

### Qué mide Paperclip (o Javier a mano hasta que esté)
- Tokens consumidos por agente por día.
- Tareas completadas vs. pendientes.
- Tiempo de respuesta a eventos disparadores.
- Tasa de escalation al humano (CEO o Javier).
- Costo en USD por agente por mes.

### Alertas
- Agente que consume > 150% de su budget sin tareas proporcionales → revisión.
- Agente con 0 actividad en ventana activa > 3 días → revisión.
- Agente con tasa de escalation > 30% → su instructions.md necesita refinement.

---

## Cambios al heartbeat

Cualquier cambio a este policy requiere:
1. Justificación (por qué la ventana actual no funciona).
2. Propuesta (nueva ventana + impacto de costo).
3. Approval del CEO agent.
4. Si cambia costo > 500 USD/mes: approval de Javier.

---

## Ver también

- `/paperclip/approvals-policy.md`
- `/paperclip/ceo-instructions.md`
- Todos los `*-instructions.md`.
- `/paperclip/tool-access-matrix.md`
