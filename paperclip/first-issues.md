# First Issues — Issues de arranque en Paperclip

Lista de issues que se crean el día 0 cuando se instala Paperclip. Cada uno es una tarea concreta que pone la máquina en marcha.

## Cómo usar este documento

En Paperclip, crear un issue por cada entrada de abajo. Asignar al agente responsable. Fecha límite: dentro de los primeros 7 días de setup.

---

## Bloque A — Fundaciones (Javier)

### A1 — Definir CEO agent
- **Asignado:** Javier (crea el agente).
- **Deadline:** Día 0.
- **Descripción:** Crear agente "CEO" en Paperclip con el prompt de `/paperclip/ceo-instructions.md`.
- **Criterio de terminación:** agente testeable con "status de la firma".

### A2 — Definir los 6 agentes subordinados
- **Asignado:** Javier + CEO agent.
- **Deadline:** Día 1-2.
- **Descripción:** Crear CRO, Head of AI Audit, CTO, COO, CMO, Client Success con sus respectivos instructions.md.
- **Criterio:** los 6 responden coherentemente a un "hola, ¿quién sos?".

### A3 — Cargar knowledge base en cada agente
- **Asignado:** Javier.
- **Deadline:** Día 2.
- **Descripción:** Cada agente tiene acceso a su carpeta relevante (ej: CRO lee `/sales/`, Head Audit lee `/audit/`).
- **Criterio:** cada agente puede citar documentos de su dominio sin errores.

### A4 — Configurar heartbeat policies
- **Asignado:** Javier.
- **Deadline:** Día 3.
- **Descripción:** Seguir `/paperclip/heartbeat-policy.md`.
- **Criterio:** CRO activa de 9 AM a 18 PM, CTO on-call durante sprints, CEO lunes + viernes.

### A5 — Approvals policy
- **Asignado:** Javier.
- **Deadline:** Día 3.
- **Descripción:** Configurar aprobaciones obligatorias según `/paperclip/approvals-policy.md`.
- **Criterio:** envío de contrato, gasto > 1K, contratación — todos requieren approval humano.

---

## Bloque B — Pipeline de Sales (CRO agent)

### B1 — Armar base Dream 100 property management
- **Asignado:** CRO.
- **Deadline:** Semana 1.
- **Descripción:** 100 empresas + 100 contactos en Miami, Orlando, Tampa, Dallas, Houston, Austin, Phoenix, LA, Denver, Atlanta, Charlotte. Fuente: LinkedIn + Apollo + directorios sectoriales.
- **Criterio:** CSV con columnas de `/sales/niches.md#estructura-de-la-lista`. 100% con email verificado.

### B2 — Configurar Instantly + dominios
- **Asignado:** CRO + COO.
- **Deadline:** Semana 1-2.
- **Descripción:** 3-5 dominios secundarios, 2 inboxes/dominio, SPF/DKIM/DMARC, 3-4 semanas warmup, volumen inicial 25-40 emails/inbox/día.
- **Criterio:** primer batch de 100 emails enviable en semana 3.

### B3 — Cargar campaña PM-E1 a PM-E4
- **Asignado:** CRO.
- **Deadline:** Semana 3.
- **Descripción:** Cargar secuencia de 4 toques en Instantly con templates de `/sales/offer-scripts.md` + `/sales/campaign-templates.md`.
- **Criterio:** primer batch enviado; tracking activo.

### B4 — Setup LinkedIn outbound
- **Asignado:** CRO.
- **Deadline:** Semana 2.
- **Descripción:** Sales Navigator + HeyReach o manual. Secuencia de 5 pasos.
- **Criterio:** 20 connections/día configurado.

### B5 — Setup CRM
- **Asignado:** CRO.
- **Deadline:** Semana 1.
- **Descripción:** Elegir (Close / HubSpot free / Airtable custom). Definir stages: `lead → replied → qualified → discovery scheduled → discovery done → audit proposed → audit closed → implementation`.
- **Criterio:** pipeline visible + primer prospecto cargado.

---

## Bloque C — Delivery ready (Head of Audit + CTO)

### C1 — Crear templates maestros del audit
- **Asignado:** Head of Audit.
- **Deadline:** Semana 1.
- **Descripción:** Crear los templates físicos del audit:
  - `ROI_Calculator_MASTER.xlsx`.
  - `Audit_Deck_MASTER.pptx`.
  - `Audit_Proposal_MASTER.docx`.
  - `Business_Map_MASTER.excalidraw`.
- **Criterio:** templates en `/assets/` usables con placeholder vars.

### C2 — Preparar stack técnico de delivery
- **Asignado:** CTO.
- **Deadline:** Semana 2.
- **Descripción:** Cuentas activas en: OpenAI/Anthropic, Supabase / Pinecone, n8n cloud, Vercel, GitHub org.
- **Criterio:** primer n8n workflow "hello world" corriendo.

### C3 — Vault de credenciales
- **Asignado:** COO + CTO.
- **Deadline:** Semana 1.
- **Descripción:** 1Password / Bitwarden team. Convenciones de naming y sharing.
- **Criterio:** todos los secrets actuales migrados.

### C4 — Crear primer client pod template
- **Asignado:** Head of Audit.
- **Deadline:** Semana 2.
- **Descripción:** Crear folder template `/delivery/client_pods_template/` con estructura de subfolders y README.md poblado.
- **Criterio:** clonable en un comando cuando llegue cliente 1.

---

## Bloque D — Marketing ligero (CMO agent)

### D1 — Perfil LinkedIn de Javier optimizado
- **Asignado:** CMO + Javier.
- **Deadline:** Semana 1.
- **Descripción:** Headline, about, featured con positioning de JM. Ver `/company/positioning.md`.
- **Criterio:** perfil refleja "AI Consulting ROI-first para property management / accounting".

### D2 — Primer post LinkedIn
- **Asignado:** CMO + Javier.
- **Deadline:** Semana 1.
- **Descripción:** Post inaugural: "arranco JM Consulting — qué hacemos y qué NO". Sin humo.
- **Criterio:** post publicado con engagement > 20 likes.

### D3 — Newsletter setup
- **Asignado:** CMO.
- **Deadline:** Semana 2.
- **Descripción:** Beehiiv / Substack configurado. Página de signup lista.
- **Criterio:** URL compartible + primer suscriptor (Javier).

### D4 — Landing page mínima de JM
- **Asignado:** CMO + CTO.
- **Deadline:** Semana 4.
- **Descripción:** Página simple (Notion / Framer / Webflow). Headline + 3 servicios + contact. Ver `/company/positioning.md`.
- **Criterio:** URL pública con form de contacto funcionando.

---

## Bloque E — Operaciones internas (COO agent)

### E1 — Billing setup
- **Asignado:** COO.
- **Deadline:** Semana 1-2.
- **Descripción:** Stripe / Wise / Mercury configurado. Templates de invoice.
- **Criterio:** primer invoice de prueba a mí mismo emitido y recibido.

### E2 — Tracker financiero
- **Asignado:** COO.
- **Deadline:** Semana 2.
- **Descripción:** Airtable o Notion con tabla de revenue, costos, runway.
- **Criterio:** snapshot mensual generable en 5 min.

### E3 — SOPs iniciales
- **Asignado:** COO.
- **Deadline:** Semana 3.
- **Descripción:** Escribir SOP-01 a SOP-04 de `/paperclip/coo-instructions.md`.
- **Criterio:** SOPs accesibles a todos los agentes.

### E4 — Contratos base
- **Asignado:** COO + Javier + abogado externo.
- **Deadline:** Semana 3.
- **Descripción:** Template de SOW, MSA, NDA, DPA en inglés y español.
- **Criterio:** 4 documentos revisados por legal + guardados.

---

## Bloque F — n8n workflows (CTO)

### F1 — Workflow 01: Nuevo lead → CRM + agente
- **Asignado:** CTO.
- **Deadline:** Semana 3.
- **Descripción:** Cuando llega un reply positivo en Instantly, crear lead en CRM + notificar al CRO agent + agendar follow-up.
- **Criterio:** testeado con lead sintético.

### F2 — Workflow 02: Discovery call → transcript + summary
- **Asignado:** CTO.
- **Deadline:** Semana 4.
- **Descripción:** Graba call (Fireflies / Otter) → transcribe → LLM genera summary con next steps → carga en CRM + client pod.
- **Criterio:** testeado con call real.

### F3 — Workflow 03: Onboarding cliente
- **Asignado:** CTO.
- **Deadline:** Semana 4-5.
- **Descripción:** Al firmar SOW, crear client pod, Slack channel, invoices, calendar kickoff.
- **Criterio:** primer cliente procesable end-to-end.

### F4 — Workflow 04: Maintenance reporting
- **Asignado:** CTO.
- **Deadline:** Mes 2.
- **Descripción:** Pull mensual de métricas de cada cliente activo + alert si alguna fuera de rango.
- **Criterio:** primer monthly review con data agregada automáticamente.

---

## Orden sugerido de ejecución

```
Semana 1: A1-A5, B5, C3, D1, E1
Semana 2: B1, B4, B5, C1, C2, C4, D3, E2
Semana 3: B2, B3, E3, E4, F1
Semana 4: C1 (finish), D4, F2, F3
Mes 2: F4, postergados
```

---

## Criterio de "firma lista para cerrar cliente 1"

Al final del mes 1, debe cumplirse:
- [ ] 6 agentes activos + testeados.
- [ ] 100 prospectos property mgmt cargados en pipeline.
- [ ] Primera secuencia de emails enviada.
- [ ] Templates de audit listos.
- [ ] Stack técnico activo.
- [ ] Landing + LinkedIn posteando.
- [ ] Billing y contratos operativos.
- [ ] Primer n8n workflow corriendo.

Cuando se cumplan todos, el CEO marca "fase 1 cerrada" y arranca "fase 2: cerrar primer cliente".

---

## Ver también

- `/paperclip/ceo-instructions.md`
- Todos los otros `*-instructions.md`.
- `/paperclip/tool-access-matrix.md`
- `/paperclip/approvals-policy.md`
- `/paperclip/heartbeat-policy.md`
