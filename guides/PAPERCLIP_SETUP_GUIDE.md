# Guía de Setup: Paperclip para JM Consulting

**Objetivo:** que en 2-3 horas tengas Paperclip corriendo con los 6 agentes (CEO, CRO, Head of Audit, CTO, COO, CMO, Client Success) leyendo sus instrucciones desde este repositorio, con heartbeat configurado y políticas de aprobación activas.

**Precondición:** este folder (`JM_Consulting_OS`) está sincronizado a OneDrive, Google Drive o accesible desde la máquina donde corre Paperclip. Todas las rutas en esta guía asumen ese directorio raíz.

---

## 0. Antes de empezar

Preparar estas tres cosas:

1. **Cuenta Paperclip activa** con plan que soporte al menos 6 agentes concurrentes y archivos adjuntos permanentes.
2. **Credenciales**: Gmail (javiercm1221.jm@gmail.com), Slack workspace JM (si ya está creado, si no lo creamos en la guía de conectores), CRM (HubSpot Starter o Attio Free), LinkedIn con sesión iniciada.
3. **Un horario de 2-3 horas** para hacer todo de una vez sin interrupciones. Setup a medias deja agentes con contexto parcial y eso se nota en la calidad de outputs.

---

## 1. Crear la organización en Paperclip

1. Abrir Paperclip → **New Organization** → nombre: `JM Consulting`.
2. Ajustes de la organización:
   - Timezone: `America/New_York` (todos los agentes usan esta TZ como referencia — ver `/paperclip/heartbeat-policy.md`).
   - Working hours: 07:00-20:00 ET lunes a sábado; domingos modo on-call.
   - Idioma por default: español (Rioplatense). Agentes que atienden clientes US: inglés americano.
3. Invitar a Javier Castro Marra (javiercm1221.jm@gmail.com) como **Owner**.

---

## 2. Subir los documentos base como Knowledge Files

Estos son los archivos que **todos** los agentes necesitan leer. Se suben una vez a la organización y se referencian desde cada agente:

| Archivo | Ubicación en el repo |
|---|---|
| Mission & Vision | `/company/mission_vision.md` |
| Core Values | `/company/core_values.md` |
| Org Chart | `/company/org_chart.md` |
| Pricing & Service Ladder | `/company/pricing_service_ladder.md` |
| Heartbeat Policy | `/paperclip/heartbeat-policy.md` |
| Approvals Policy | `/paperclip/approvals-policy.md` |
| Glosario JM | `/company/glossary.md` |
| Código de conducta con clientes | `/company/client_conduct.md` |

En Paperclip: **Organization → Knowledge → Add files**. Subir cada uno. Marcarlos como "Shared with all agents".

---

## 3. Crear los 6 agentes

Para cada agente el procedimiento es el mismo:

1. **Agents → New Agent**.
2. Nombre, rol y avatar (podés generar avatares con IA o usar iniciales).
3. Pegar el contenido de `/paperclip/agents/<agent>.md` en el campo **System Instructions**.
4. Adjuntar los Knowledge Files específicos del agente (ver tabla abajo).
5. Configurar heartbeat (ver sección 4).
6. Configurar aprobaciones (ver sección 5).
7. Conectar herramientas (ver `CONNECTORS_SETUP_GUIDE.md`).

### 3.1 CEO Agent · "Alex"

- Instructions: `/paperclip/agents/ceo.md`
- Knowledge extra: `/company/pricing_service_ladder.md`, `/sales/pipeline-methodology.md`, `/maintenance/retainer-tiers.md`, `/paperclip/heartbeat-policy.md`, `/paperclip/approvals-policy.md`.
- Rol en la org: aprueba Nivel 1, delega a Javier para Nivel 2, coordina heartbeat semanal.

### 3.2 CRO Agent · "Sol"

- Instructions: `/paperclip/agents/cro.md`
- Knowledge extra: `/sales/icp-verticals.md`, `/sales/qualification-framework.md`, `/sales/outbound-playbook.md`, `/n8n/sales-engine-spec.md`, `/assets/One_Pager_JM.md`.
- Herramientas que necesita (paso posterior): Instantly, Apollo, Clay, HeyReach, Fireflies, CRM, Slack.

### 3.3 Head of Audit · "Andrés"

- Instructions: `/paperclip/agents/head-of-audit.md`
- Knowledge extra: `/audit/methodology.md`, `/audit/discovery-scripts.md`, `/audit/opportunity-matrix-rubric.md`, `/audit/roi-calculator-usage.md`, `/assets/ROI_Calculator_MASTER.xlsx`, `/assets/Audit_Deck_MASTER.pptx`, `/assets/Audit_Proposal_MASTER.docx`.
- Herramientas: Fireflies (transcripts), Google Drive (plantillas), Claude (redacción), Excel (cálculos).

### 3.4 CTO Agent · "Tomás"

- Instructions: `/paperclip/agents/cto.md`
- Knowledge extra: `/delivery/stack-guidelines.md`, `/delivery/eval-framework.md`, `/n8n/workflow-inventory.md`, `/n8n/sales-engine-spec.md`, `/n8n/support-agent-spec.md`, `/n8n/onboarding-workflow-spec.md`, `/n8n/maintenance-reporting-spec.md`.
- Herramientas: n8n MCP, Supabase MCP, GitHub, Claude Code.

### 3.5 COO Agent · "Clara"

- Instructions: `/paperclip/agents/coo.md`
- Knowledge extra: `/delivery/sprint-playbook.md`, `/delivery/rollout-policy.md`, `/maintenance/sla-matrix.md`, `/paperclip/heartbeat-policy.md`.
- Herramientas: Notion/Asana, Slack, Google Calendar, Stripe.

### 3.6 CMO Agent · "Mei"

- Instructions: `/paperclip/agents/cmo.md`
- Knowledge extra: `/sales/content-calendar.md`, `/sales/positioning.md`, `/assets/One_Pager_JM.html`, `/assets/One_Pager_JM.md`.
- Herramientas: LinkedIn (via HeyReach), Substack/blog, Notion, Slack.

### 3.7 Client Success Agent · "Luca"

- Instructions: `/paperclip/agents/client-success.md`
- Knowledge extra: `/maintenance/mbr-template.md`, `/maintenance/runbooks/`, `/n8n/maintenance-reporting-spec.md`, `/delivery/handoff-checklist.md`.
- Herramientas: Slack, Gmail, Fireflies, CRM, dashboards de clientes.

---

## 4. Configurar heartbeat por agente

El heartbeat es el latido: cuándo el agente se despierta solo, chequea su contexto, y empuja acciones. La política completa está en `/paperclip/heartbeat-policy.md`, acá va el resumen operativo:

| Agente | Modo por default | Frecuencia | Triggers event-driven |
|---|---|---|---|
| CEO (Alex) | Rhythmic | Lunes 08:00 ET (weekly review) + jueves 17:00 ET (gap check) | Deal cerrado > 10K; alerta roja de cliente; PRs críticos en repo |
| CRO (Sol) | Rhythmic | Cada día 09:00 + 14:00 ET | Lead nuevo en Instantly; reply positivo en cold; Fireflies publica transcript |
| Head of Audit (Andrés) | Event-driven | N/A | Kickoff audit; sesión nueva en Fireflies de audit; deadline proposal |
| CTO (Tomás) | Rhythmic | Lunes y jueves 10:00 ET | Workflow en error en n8n; deploy a producción; alerta de costs monitor |
| COO (Clara) | Rhythmic | Diario 08:30 ET | Invoice creada; SLA > 80% consumido; nuevo cliente firmado |
| CMO (Mei) | Rhythmic | Martes y viernes 11:00 ET | Post con engagement > 500; menciones de marca; nuevo case study cerrado |
| Client Success (Luca) | On-call | — | Alerta de salud cliente; ticket de soporte escalado; MBR mensual |

**Cómo configurar en Paperclip:**

1. Abrir el agente → **Settings → Heartbeat**.
2. Elegir modo: `Rhythmic` / `Event-driven` / `On-call`.
3. Si rhythmic: definir cron (Paperclip acepta cron estándar o lenguaje natural "every weekday at 9am ET").
4. Si event-driven: listar los webhooks/triggers que lo despiertan (esos los implementamos en n8n, ver guía de conectores).
5. Activar **Quiet mode**: sábados 20:00 → lunes 06:00 ET (nadie emite acciones externas salvo on-call).

---

## 5. Configurar aprobaciones

La política completa vive en `/paperclip/approvals-policy.md`. Resumen operativo:

- **Nivel 0 (autónomo)**: agente actúa sin preguntar. Ejemplos: borradores de email interno, enriquecimiento de leads, updates de CRM, sync de calendarios.
- **Nivel 1 (CEO agent aprueba)**: descuentos hasta 15%, compromisos de entrega, cambios de scope < 5K, posteos en LinkedIn de marca JM.
- **Nivel 2 (Javier aprueba)**: descuentos > 15%, compromisos > 10K, cambios de pricing, firma de SOW, hire/fire, gastos > 500 USD, crisis pública.

**Cómo configurar en Paperclip:**

1. Abrir cada agente → **Settings → Approvals**.
2. Definir tipos de acción y nivel requerido (Paperclip usa tags; podés etiquetar "discount", "commitment", "public-post", etc.).
3. Enlazar el CEO agent como approver de Nivel 1.
4. Enlazar el email de Javier como approver de Nivel 2 (llega como notificación a Slack + email).
5. Definir SLA de respuesta: Nivel 1 < 2 horas laborales; Nivel 2 < 12 horas laborales. Si no hay respuesta, se escala automáticamente al siguiente nivel o se congela la acción.

---

## 6. Crear los "Pods" de cliente

Cada cliente que firma audit o sprint tiene un **Pod**: un espacio de colaboración en Paperclip que agrupa los agentes relevantes + archivos del cliente + heartbeat específico.

Plantilla ya existe en: `/client_pods_template/`. Estructura:

```
/client_pods/<client-slug>/
  ├── 00_context/           # SOW, discovery transcripts, diagramas
  ├── 01_audit/             # Outputs del audit: deck, proposal, ROI calc
  ├── 02_delivery/          # Sprint playbook, workstream docs
  ├── 03_maintenance/       # MBRs, runbooks, dashboards
  ├── 04_comms/             # Emails, Slack threads relevantes
  └── README.md             # Estado del pod, próximo milestone, owner
```

Cuando firma un cliente nuevo:

1. Crear folder siguiendo el template (copiar `client_pods_template` y renombrar).
2. En Paperclip, crear un **Project** con el mismo nombre y vincular esa carpeta como Knowledge.
3. Asignar agentes al project: siempre Head of Audit + CTO + Client Success. COO entra para billing y SLAs. CRO entra para upsells.
4. Configurar heartbeat específico del pod: cadencia de status weekly para Javier.

---

## 7. Tests de humo

Antes de darlo por terminado, correr estos 5 tests. Si alguno falla, revisar instrucciones y archivos adjuntos:

**Test 1 — CEO conoce el service ladder**
Preguntar al CEO agent: *"¿Cuáles son los 4 tiers del service ladder y a qué precio cada uno?"*
Esperado: Audit 10K, Sprint 10-20K, Strategic 25K+, Retainer 2-50K/mes.

**Test 2 — CRO arma un outbound draft**
Pedir al CRO: *"Armame un cold email para un Controller de una Property Management firm de 15M ARR que maneja ~120 propiedades. Foco en reducir tiempo de lease renewal emails."*
Esperado: email ROI-first, específico, con hook de benchmark y CTA a 15-min call.

**Test 3 — Head of Audit explica la metodología**
Preguntar: *"Explicame en 6 puntos el flujo del audit de 10 días."*
Esperado: outcomes → business map → task map → feasibility → opportunity matrix → ROI.

**Test 4 — CTO identifica riesgos técnicos**
Pedir: *"Si un cliente quiere loop cerrado en lead response desde día 1, ¿qué riesgos planteás y cómo los mitigás?"*
Esperado: riesgos de accuracy sin human-in-loop, riesgo de alucinación en respuestas, riesgo de compliance; mitigaciones: rollout canary, eval framework, escalation gates.

**Test 5 — Approvals funciona**
Pedir al CRO: *"Ofrecele 25% de descuento a XYZ para cerrar esta semana."*
Esperado: el CRO responde que Nivel 2 requiere aprobación de Javier y lanza la notificación.

---

## 8. Mantenimiento del setup

- **Mensual**: revisar transcripts de heartbeat semanal. ¿Los agentes están accionando lo correcto? ¿Hay drift vs. las instrucciones?
- **Trimestral**: revisar cada `/paperclip/agents/*.md` y actualizar si cambió el negocio. Re-subir a Paperclip (los agentes NO releen automáticamente — hay que forzar el reload).
- **Por evento**: si cambia pricing, contratación, o un workflow core, actualizar el archivo relevante y reindexar knowledge.

---

## 9. Troubleshooting

**"El agente ignora las instrucciones."**
Revisar que el archivo esté bien adjunto y que el agente tenga permisos de lectura. En Paperclip a veces un adjunto se "desvincula" tras un update.

**"El agente da respuestas genéricas tipo ChatGPT."**
Falta contexto vertical. Adjuntar los docs específicos del vertical del cliente (ej. `/audit/verticals/property-management.md`).

**"Heartbeat no se dispara."**
Chequear en Paperclip → Agent → Logs. Si el webhook viene de n8n y no llega, verificar que la workflow esté **Active** y el endpoint esté bien configurado.

**"Aprobación colgada."**
SLA expiró sin respuesta: Paperclip debería escalar solo. Si no lo hace, revisar la configuración del approver (email válido, notificaciones habilitadas).

---

## 10. Próximo paso

Una vez Paperclip está andando, seguí con `CONNECTORS_SETUP_GUIDE.md` para conectar Instantly, Apollo, Clay, Apify, HeyReach, LinkedIn, Stripe, Slack, Drive, Supabase, n8n, 1Password y Fireflies. Sin conectores los agentes existen pero no pueden ejecutar nada fuera de Paperclip.
