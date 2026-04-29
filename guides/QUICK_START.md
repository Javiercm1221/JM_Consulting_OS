# Quick Start — JM Consulting OS

Llegaste acá porque querés arrancar. Este documento es la hoja de ruta condensada.

## ¿Qué es esto?

Un operating system completo para JM Consulting: documentos, procesos, agentes de Paperclip, workflows de n8n, activos comerciales y guías de setup. Todo diseñado para que un solo founder (Javier) corra una consultora de AI de 200-500K USD de ARR con 3-6 agentes autónomos y 20 workflows de n8n haciendo el trabajo operativo.

## Arquitectura en una frase

**Claude diseña · Paperclip organiza · n8n ejecuta.**

## Estructura del repo

```
JM_Consulting_OS/
├── 00_MASTER/           # Documentos fundacionales (manifesto, strategy, principles)
├── company/             # Mission, vision, values, org, pricing, glosario
├── sales/               # ICP, playbook outbound, qualifying, pipeline methodology
├── audit/               # Metodología del audit 10 días, rúbricas, scripts
├── delivery/            # Sprint playbook, eval framework, rollout policy
├── maintenance/         # SLA matrix, retainer tiers, runbooks, MBR template
├── paperclip/           # Instructions de los 6 agentes + heartbeat + approvals policy
├── n8n/                 # 10 workflows internos + 10 workflows de cliente (specs)
├── assets/              # ROI Calculator, Audit Deck, Proposal, One-Pager
├── client_pods_template/ # Template para cada cliente nuevo
└── guides/              # Setup guides (Paperclip, conectores, este quick-start)
```

## Orden de lectura recomendado (2 horas)

1. **Leer `company/mission_vision.md` + `company/core_values.md`** → qué es JM y por qué.
2. **Leer `company/pricing_service_ladder.md`** → modelo de negocio en 4 tiers.
3. **Leer `audit/methodology.md`** → el core del producto, el audit de 10 días.
4. **Hojear `paperclip/agents/*.md`** → quiénes son los 6 agentes y qué hacen.
5. **Hojear `n8n/workflow-inventory.md`** → qué automatizamos.
6. **Abrir los 4 assets en `/assets/`** → lo que le mostrás al cliente.

## Orden de implementación (4 semanas)

**Semana 1 — Setup base**
- Seguir `guides/PAPERCLIP_SETUP_GUIDE.md` (2-3 hs).
- Seguir `guides/CONNECTORS_SETUP_GUIDE.md` sección 1-9 (críticos).
- Probar: discovery call grabada en Fireflies → JM-02 genera summary → aterriza en Paperclip.

**Semana 2 — Primer audit real**
- Identificar 3 prospects de ICP (Property Mgmt o Accounting).
- Outbound manual (1 touch cada uno) usando el one-pager.
- Agendar 1 discovery call → usar script de `audit/discovery-scripts.md`.
- Arrancar el audit siguiendo `audit/methodology.md`.

**Semana 3 — Primer sprint + sales engine arranca**
- Si el audit cerró: arrancar Quick Wins Sprint siguiendo `delivery/sprint-playbook.md`.
- En paralelo: conectar Instantly + Apollo + empezar warming de dominios.

**Semana 4 — Handoff + retainer**
- Sprint en producción con canary rollout.
- Primer MBR template corrido vía JM-04.
- Cliente entra a retainer Tier 1/2.

## Stop rules (cuándo pausar y pensar)

- **Si el primer audit no cierra sprint**: revisar `audit/opportunity-matrix-rubric.md` — puede que estés eligiendo oportunidades con ROI débil.
- **Si el outbound genera < 5 replies en 200 emails**: el problema es ICP o subject line, no volumen. Revisar `sales/icp-verticals.md`.
- **Si un workflow de cliente acumula > 20 errores/semana**: parar, hacer root cause, no parchar. El eval framework en `delivery/eval-framework.md` está para esto.

## Deliverables listos para usar

Los 4 masters ya están en `/assets/`:

- **ROI Calculator** (`ROI_Calculator_MASTER.xlsx`) — 8 sheets, 117 formulas, cambiá los inputs del cliente en `Supuestos` y el resto recalcula.
- **Audit Deck** (`Audit_Deck_MASTER.pptx`) — 22 slides, brandeado Midnight Executive. Solo cambiás cliente, vertical, y específicos.
- **Audit Proposal** (`Audit_Proposal_MASTER.docx`) — 10 secciones, lista para mandar con el audit.
- **One-Pager** (`One_Pager_JM.html` + `.md`) — para mandar al prospect antes de la discovery call.

Abrí `ROI_Calculator_MASTER.xlsx`, andá al sheet `Dashboard` y vas a ver cómo los números del audit se traducen en la conversación comercial.

## Contacto operativo

Javier Castro Marra · Founder
javiercm1221.jm@gmail.com

**Cualquier cambio estratégico (pricing, nuevo vertical, cambio de stack) se edita en el archivo fuente y se re-sincroniza a Paperclip reindexando knowledge. Los agentes no releen solos.**
