# Organigrama — JM Consulting

Organización operada principalmente por agentes en Paperclip. Humano = Javier (owner / CEO real). Los roles descritos son **agentes** que reportan a Javier.

## Nivel 1 — Ejecutivo

### CEO (agente)
- Misión general, prioridades, contratación de nuevos agentes, coordinación.
- Heartbeat durante setup: cada 600 s.
- Heartbeat estable: cada 1800-3600 s.
- Aprueba manualmente nuevas contrataciones de agentes y acciones delicadas al inicio.

### CRO / Revenue Director
- Dueño de: nichos, scraping, campañas outbound, reuniones, pipeline comercial.
- Herramientas: Apify, Vibe Prospecting, Apollo, Gmail / Resend, Instantly, Sheets / Airtable / CRM.
- Heartbeat setup: 600-900 s. Estable: según necesidad.

**Subagentes del CRO:**
- Prospect Research Agent
- Lead Enrichment Agent
- Outreach Campaign Agent
- CRM & Inbox Agent

### Head of AI Audit
- Dueño de: entrevistas, discovery, outcome definition, business mapping, task mapping, opportunity matrix, ROI y recomendaciones.
- Herramientas: Brave Search, documentos, email, templates de entrevistas, calculadora ROI.
- Heartbeat setup: 600-900 s.

**Subagentes del Head of AI Audit:**
- Interview Designer
- Process Mapper
- ROI Analyst
- Opportunity Prioritization Agent

### CTO / Automation Architect
- Dueño de: diseño técnico, arquitectura de n8n, prompts, integraciones, QA, handoff técnico.
- Herramientas: Brave Search, Resend, n8n, repositorio y APIs.
- Heartbeat setup: 600-900 s.

**Subagentes del CTO:**
- Workflow Builder
- Integration Agent
- Testing & QA Agent
- Prompt / Knowledge Agent

### COO / Delivery Director
- Dueño de: cronogramas, handoff entre ventas y delivery, estado de proyectos, seguimiento de tasks, documentación operativa.
- Herramientas: email, documentación, gestor de tareas, reportes.
- Heartbeat setup: 900-1800 s.

**Subagentes del COO:**
- Onboarding Agent
- Project Tracking Agent
- Documentation Agent

### CMO / Authority & Content Director
- Dueño de: branding, casos de estudio, contenido, newsletters, materiales comerciales, demos visuales.
- Herramientas: Brave Search, Resend, bases de contenido, website / CMS.
- Heartbeat setup: 900-1800 s.

**Subagentes del CMO:**
- Research Content Agent
- Case Study Writer
- Offer Packaging Agent

### Client Success & Maintenance Lead
- Dueño de: seguimiento post implementación, soporte, mejora continua, reportes mensuales, nuevas oportunidades.
- Herramientas: email, reporting, dashboards, documentación del cliente.
- Heartbeat: 1800-3600 s.

**Subagentes del CS Lead:**
- Health Check Agent
- Reporting Agent
- Upsell Opportunity Agent

## Orden de contratación (agentes imprescindibles al inicio)

**Bloque 1 (arranque):** CEO · CRO · Head of AI Audit · CTO · COO · CMO.

**Bloque 2 (cuando hay 1er cliente):** Client Success Lead · Prospect Research Agent · ROI Analyst · Workflow Builder · Documentation Agent.

**Bloque 3 (escala):** resto de subagentes a medida que crece el pipeline.

## Los 6 agentes de negocio (capa funcional, no jerárquica)

Además del organigrama, en documentación interna se usan estas 6 etiquetas funcionales:

1. **Hustler** — prospección (mapea al CRO).
2. **Rainmaker** — sales enablement (mapea a CRO + CMO).
3. **Operator** — delivery (mapea a COO + CTO).
4. **Storyteller** — marketing (mapea al CMO).
5. **Guardian** — customer support (mapea al Client Success Lead).
6. **COO** — consolidación operativa y reporting (mapea al COO).

## Aprobaciones

- Al inicio: manuales para contratación de agentes, envío de campañas outbound, publicación de contenido y facturación.
- Estable: automáticas para tareas repetitivas seguras (reporting, follow-ups). Manuales para cualquier cosa que toque dinero, cliente externo o compliance.

## Principio de operación

**Claude diseña, Paperclip organiza y visualiza, n8n ejecuta.**
