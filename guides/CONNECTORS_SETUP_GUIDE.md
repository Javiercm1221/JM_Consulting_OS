# Guía de Setup: Conectores para JM Consulting

**Objetivo:** conectar todas las herramientas que los agentes de Paperclip y los workflows de n8n necesitan para ejecutar. Al terminar vas a tener el stack operativo completo.

**Precondición:** Paperclip ya está configurado siguiendo `PAPERCLIP_SETUP_GUIDE.md`. Si no, arrancá por ahí primero.

**Tiempo estimado:** 4-6 horas. Lo crítico (Gmail, Slack, n8n, Supabase, CRM, Stripe) en 2 horas; el resto se puede hacer en días sucesivos.

---

## 0. Matriz de conectores

| # | Conector | Criticidad | Quién lo usa | Costo mensual |
|---|---|---|---|---|
| 1 | **Gmail** | Crítico | Todos + JM-01, JM-06, SE-05 | 0 (Google Workspace 6 USD/user si querés dominio propio) |
| 2 | **Slack** | Crítico | Todos + todos los workflows | 0 (Free tier alcanza los primeros 6 meses) |
| 3 | **CRM (HubSpot Starter)** | Crítico | CRO, COO, Client Success + JM-01, JM-09 | 20 USD/mes |
| 4 | **n8n (self-hosted o cloud)** | Crítico | CTO + todos los workflows | 20 USD/mes cloud o 5 USD/mes VPS |
| 5 | **Supabase** | Crítico | CTO + CL-001..010 | 0 (free tier para empezar) |
| 6 | **Stripe** | Crítico | COO + JM-06 | 0 (comisión por transacción) |
| 7 | **Google Drive** | Crítico | Todos | Incluido con Google Workspace |
| 8 | **1Password** | Crítico | Todos (secretos) | 3 USD/mes |
| 9 | **Fireflies.ai** | Alto | Head of Audit, CRO | 10 USD/mes |
| 10 | **Instantly** | Alto | CRO + SE-01 | 37 USD/mes (Growth plan) |
| 11 | **Apollo** | Alto | CRO + SE-02 | 49 USD/mes (Basic) |
| 12 | **Clay** | Medio | CRO + SE-03 | 149 USD/mes (Starter) |
| 13 | **Apify** | Medio | CRO + SE-04 | 49 USD/mes (Pay-as-you-go) |
| 14 | **HeyReach** | Medio | CMO + CRO | 79 USD/mes |
| 15 | **LinkedIn (session)** | Medio | CMO | 0 |
| 16 | **GitHub** | Bajo | CTO | 0 (free) |
| 17 | **Notion** | Bajo | COO, CMO | 0 (free plan) |

Gasto fijo mínimo viable: **~200 USD/mes**. Full stack con Clay y Apollo: **~450 USD/mes**.

---

## 1. Gmail + Google Workspace

**Objetivo:** agentes mandan emails, leen respuestas, agendan en Google Calendar.

1. Si usás javiercm1221.jm@gmail.com (consumer): alcanza para empezar pero perdés email transaccional profesional. Recomendación: **comprar dominio `jmconsulting.ai` o similar** (10-15 USD/año en Namecheap) y levantarle Google Workspace (6 USD/user/mes).
2. En Paperclip → **Integrations → Gmail** → OAuth con la cuenta.
3. En n8n → **Credentials → Google OAuth2 API** → scopes: gmail.send, gmail.modify, calendar.events.
4. Test: pedirle al COO agent *"Mandame un email de prueba a mí mismo"*.

**Nota de deliverabilidad:** para outbound masivo (Instantly) NO usar el dominio principal. Comprar 2-3 dominios secundarios (`getjm.ai`, `hey-jm.com`) con SPF/DKIM/DMARC configurados + warming de 3-4 semanas. Instantly tiene módulo de warming incluido.

---

## 2. Slack

**Objetivo:** canal central de notificaciones, aprobaciones, alertas, heartbeat reports.

1. Crear workspace `jm-consulting` si no existe.
2. Canales a crear (el bot de Paperclip los puede crear solo si le das permisos):
   - `#general` — humano
   - `#heartbeat` — outputs diarios/semanales de agentes
   - `#approvals` — requests de aprobación Nivel 1/2
   - `#alerts-prod` — alertas de n8n (errores en workflows productivos)
   - `#alerts-cost` — alertas del cost monitor (JM-08)
   - `#pipeline` — notificaciones de leads, deals, Fireflies transcripts
   - `#clients-<slug>` — uno por cliente activo (auto-creado por JM-03 onboarding workflow)
3. Instalar app oficial de Paperclip en Slack (desde el directorio de Slack).
4. En n8n → **Credentials → Slack API** → OAuth con scopes: `chat:write`, `channels:read`, `channels:manage`, `users:read`, `files:write`.
5. Test: pedirle al CEO agent *"Postea un test en #heartbeat"*.

---

## 3. CRM — HubSpot Starter

**Objetivo:** verdad única del pipeline; scoring, fuentes, stages, deals, contactos.

**Por qué HubSpot Starter y no Attio:** HubSpot tiene integraciones nativas con Instantly, Apollo, Clay, Stripe, Fireflies. Attio es más lindo pero en fase 0-50K ARR ralentiza. Pipecl después si querés.

1. Crear cuenta en hubspot.com → plan **Sales Starter** (20 USD/mes).
2. Pipelines a crear:
   - **Prospecting** (stages: New → Engaged → Qualified → Discovery → Audit → Closed)
   - **Delivery** (stages: Audit → Proposal Sent → Sprint → Implementation → Handed Off)
   - **Retainer** (stages: Tier 1 → Tier 2 → Tier 3 → Tier 4 → Churned)
3. Custom properties importantes:
   - `vertical` (dropdown: property-mgmt, accounting, legal, logistics, healthcare, manufacturing, b2b-saas, other)
   - `icp_score` (number 0-100)
   - `source` (outbound / inbound / referral / paid)
   - `audit_credit_used` (boolean)
   - `retainer_tier` (dropdown T1-T4)
4. En Paperclip → **Integrations → HubSpot** → API key + OAuth.
5. En n8n → **Credentials → HubSpot OAuth2 API**.
6. Test: pedirle al CRO *"Creame un contacto de prueba: Juan Pérez, CFO, Acme Corp, 12M ARR, vertical property management"*.

---

## 4. n8n (self-hosted recomendado)

**Objetivo:** motor de ejecución de los 20 workflows (JM-01..10 internos + CL-001..010 de clientes).

**Opciones:**
- **n8n Cloud (20 USD/mes)**: setup instantáneo, pero límites de ejecuciones. Bueno para arrancar.
- **Self-hosted en VPS**: Hetzner (4.5 USD/mes) + Docker. Más laburo inicial pero escala infinito.

**Recomendación:** empezar con n8n Cloud 20 USD/mes; migrar a self-hosted cuando superes 5 clientes activos.

**Setup cloud:**

1. Crear cuenta en n8n.cloud.
2. En Paperclip → integrar n8n como MCP (Paperclip tiene conector nativo).
3. Importar los specs de workflows desde `/n8n/workflow-inventory.md` — para cada uno: crear workflow nuevo y seguir la estructura descrita.
4. Priorizar implementación en este orden:
   - **Semana 1**: JM-01 (lead capture), JM-02 (discovery summary), JM-10 (heartbeat monitor).
   - **Semana 2**: JM-03 (onboarding), JM-06 (invoice follow-up).
   - **Semana 3**: JM-04 (maintenance reporting), JM-08 (cost monitoring).
   - **Semana 4**: SE-01..06 (sales engine) si ya tenés Instantly/Apollo contratado.
5. Para cada workflow activo: configurar Slack notification en error → canal `#alerts-prod`.

**Setup self-hosted (más adelante):**

```bash
# En un VPS Ubuntu 22.04
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  -e N8N_BASIC_AUTH_ACTIVE=true \
  -e N8N_BASIC_AUTH_USER=javier \
  -e N8N_BASIC_AUTH_PASSWORD='<strong-pw>' \
  -e WEBHOOK_URL=https://n8n.jmconsulting.ai/ \
  docker.n8n.io/n8nio/n8n
```

Apuntar dominio con Cloudflare → VPS IP. SSL con Caddy o Traefik.

---

## 5. Supabase

**Objetivo:** base de datos compartida para workflows de cliente (CL-001..010) — logs, conversaciones, eventos, embeddings para RAG si aplica.

1. Crear cuenta en supabase.com → plan **Free** (suficiente para empezar).
2. Crear proyecto: `jm-consulting-shared` (los clientes grandes van a tener su propio proyecto después).
3. Tablas base a crear:
   - `events` (id, client_slug, event_type, payload jsonb, created_at)
   - `conversations` (id, client_slug, channel, user_id, messages jsonb, status, created_at)
   - `evals` (id, client_slug, workflow, input, expected, actual, score, passed, created_at)
   - `costs` (id, client_slug, workflow, model, tokens_in, tokens_out, cost_usd, created_at)
4. RLS: deshabilitado al inicio, habilitar cuando onboardeás primer cliente con sus propias credenciales.
5. En Paperclip → integrar Supabase MCP (conector ya disponible en tus MCPs).
6. En n8n → **Credentials → Supabase** → URL del proyecto + service role key (guardar en 1Password).

---

## 6. Stripe

**Objetivo:** emisión de invoices, cobro de audits, retainers mensuales.

1. Crear cuenta en stripe.com (activar modo live cuando tengas primer cliente firmado; hasta ahí, test mode).
2. Productos a crear:
   - `AI_OPPORTUNITY_AUDIT_10K` — one-time 10,000 USD
   - `QUICK_WINS_SPRINT_10K`, `_15K`, `_20K` — one-time
   - `STRATEGIC_IMPL_25K`, `_35K`, `_50K` — one-time (o en 2-3 cuotas)
   - `RETAINER_T1_2K`, `T2_5K`, `T3_10K`, `T4_20K`, `T4_50K` — recurring monthly
3. Webhook endpoints a configurar apuntando a n8n:
   - `invoice.paid` → JM-06 (marca invoice como paid en CRM)
   - `invoice.payment_failed` → JM-06 (arma email de follow-up)
   - `customer.subscription.deleted` → alerta de churn a `#alerts-prod`
4. En Paperclip → **Integrations → Stripe** → API key (restricted, solo con permisos de invoices y customers).
5. En n8n → **Credentials → Stripe API**.

---

## 7. Google Drive

**Objetivo:** storage compartido de deliverables del audit, pod de cliente, assets.

1. Crear carpeta compartida `JM Consulting — Client Deliverables` en Drive.
2. Subcarpetas:
   - `_templates/` — plantillas master (audit deck, proposal, ROI calc)
   - `_active/<client-slug>/` — un folder por cliente activo
   - `_archive/<year>/<client-slug>/` — clientes cerrados
3. En Paperclip → **Integrations → Google Drive** → OAuth.
4. En n8n → **Credentials → Google Drive OAuth2**.
5. Copiar los masters a `_templates/`:
   - `/assets/Audit_Deck_MASTER.pptx` → Drive
   - `/assets/Audit_Proposal_MASTER.docx` → Drive
   - `/assets/ROI_Calculator_MASTER.xlsx` → Drive
   - `/assets/One_Pager_JM.md` + `.html` → Drive

---

## 8. 1Password

**Objetivo:** única fuente de secretos (API keys, passwords, tokens). Nada hardcodeado en Paperclip ni n8n fuera de referencias a 1P.

1. Crear vault `JM-Consulting-Prod`.
2. Items a crear (irás cargando a medida que conectás cada servicio):
   - Gmail API credentials
   - Slack bot token
   - HubSpot API key
   - Stripe restricted keys (test + live)
   - Supabase service role + anon keys
   - n8n admin password
   - Instantly API key
   - Apollo API key
   - Clay API key
   - Apify API token
   - HeyReach API key
   - Fireflies API token
   - OpenAI + Anthropic API keys (para n8n)
   - Dominios: credenciales de DNS (Cloudflare)
3. Activar **1Password CLI** en la máquina donde corre n8n self-hosted para inyectar secretos en runtime.
4. Compartir el vault con el agente CTO (via conector nativo si existe) o dejar que agentes pidan los secretos explícitamente cuando los necesiten.

---

## 9. Fireflies.ai

**Objetivo:** transcribir todas las discovery calls, demos, MBRs. Fuente de truth para `/audit/discovery-scripts.md` → populated con data real.

1. Crear cuenta fireflies.ai → plan **Pro** (10 USD/mes).
2. Conectar Google Calendar para que se una automáticamente a los meets.
3. Configurar workspaces/folders por cliente.
4. En n8n → webhook de Fireflies → dispara JM-02 (discovery summary) cuando se publica un nuevo transcript.
5. En Paperclip → integrar Fireflies MCP (si disponible) o vía webhook relay.

---

## 10. Instantly

**Objetivo:** motor de outbound email cold (SE-01). Warming + sending + deliverability.

1. Crear cuenta instantly.ai → plan **Growth** 37 USD/mes.
2. Conectar 2-3 inboxes de dominios secundarios (NO el principal).
3. Warming: activar 3-4 semanas antes de enviar volumen real. Empezar con 20 emails/día/inbox, escalar 5/día hasta 50.
4. Listas a crear: una por vertical ICP (property-mgmt, accounting, etc.).
5. Templates base: importar desde `/sales/outbound-playbook.md`.
6. En n8n → **Credentials → Instantly** (API key).
7. Webhook: reply event → dispara JM-01 (lead capture).

---

## 11. Apollo

**Objetivo:** sourcing de contactos (CFO, Controller, COO, Head of Ops) por vertical.

1. Crear cuenta apollo.io → plan **Basic** 49 USD/mes (10K créditos).
2. Filtros base por vertical:
   - Property Management: Industry=`Real Estate`, Size `50-500 employees`, Title=`Controller` OR `CFO` OR `Director of Operations`, Geo=`United States`.
   - Accounting Firms: Industry=`Accounting`, Size `20-200`, Title=`Partner` OR `Managing Director`.
   - (completar según `/sales/icp-verticals.md`).
3. En n8n → **Credentials → Apollo** (API key).
4. SE-02 workflow: saca lista diaria de 200 contactos nuevos que matcheen ICP → push a Clay para enrichment.

---

## 12. Clay

**Objetivo:** enrichment + scoring ICP + personalización profunda antes de Instantly.

1. Crear cuenta clay.com → plan **Starter** 149 USD/mes (dudoso ROI en mes 1, se puede posponer a mes 2-3).
2. Tables base:
   - `ICP_scoring` — input Apollo → output con signals (funding, hiring, tech stack) y score 0-100.
   - `Personalization` — input high-score contacts → genera line personalizada para el email (hook vertical-específico).
3. En n8n → HTTP node con Clay API (Clay tiene integración oficial con n8n cloud).

---

## 13. Apify

**Objetivo:** scraping de señales públicas para SE-04 (trigger events: job posts, funding announcements, press releases).

1. Crear cuenta apify.com → plan **Pay-as-you-go** (arrancá con 49 USD de créditos).
2. Actors a correr:
   - `apify/linkedin-jobs-scraper` — detecta hiring en ICP companies (signal de growth).
   - `apify/google-search-scraper` — busca "hiring AI Ops" OR "automation manager" en verticals target.
   - `apify/rag-web-browser` — para research específico de una cuenta.
3. En Paperclip → integrar Apify MCP (ya disponible).
4. En n8n → HTTP node con Apify API; SE-04 workflow schedule diario 06:00 ET.

---

## 14. HeyReach

**Objetivo:** LinkedIn outreach sistematizado (connection + follow-up + nurture).

1. Crear cuenta heyreach.io → plan **Starter** 79 USD/mes.
2. Conectar LinkedIn personal de Javier (sesión persistente, HeyReach simula actividad humana para evitar baneo).
3. Sequences base:
   - `Cold Connect` — request + 3 follow-ups.
   - `Post-engagement` — cuando alguien reacciona a un post de CMO.
   - `Post-audit` — reconnect 3 meses después de un audit que no cerró sprint.
4. En n8n → webhook HeyReach → dispara JM-01 si hay reply positivo.

---

## 15. LinkedIn (sesión directa)

**Objetivo:** postear contenido de CMO; interactuar con red; seguir ICP targets.

1. Cuenta personal Javier + Company Page `JM Consulting`.
2. **No automatizar posts directamente vía API pública** (LinkedIn restringe). Opciones:
   - Usar HeyReach (arriba) para DMs/connects.
   - Usar **Buffer** o **Typefully** (10-15 USD/mes) para scheduling de posts.
3. En Paperclip → CMO agent redacta posts, Javier (o una persona VA) los publica manualmente o usa Buffer como puente.

---

## 16. GitHub

**Objetivo:** versionado de código de n8n workflows + artefactos técnicos + instrucciones de agentes.

1. Crear organización `jm-consulting` en GitHub (free plan).
2. Repos:
   - `jm-os` — este repositorio (JM_Consulting_OS) bajo git.
   - `jm-n8n-workflows` — JSON exports de workflows.
   - `jm-client-<slug>` — privado, uno por cliente en delivery.
3. En Paperclip → CTO agent conectar GitHub MCP.
4. En n8n → credentials de deploy key por repo.

**Inicializar este folder como repo:**

```bash
cd "/c/Users/User/OneDrive/Desktop/JM Auditorias IA/JM_Consulting_OS"
git init
git add .
git commit -m "Initial commit: JM Consulting OS v1"
git remote add origin git@github.com:jm-consulting/jm-os.git
git push -u origin main
```

---

## 17. Notion (opcional pero útil)

**Objetivo:** wiki interna de procesos, runbooks, onboarding de nuevos agentes humanos.

1. Crear workspace `JM Consulting` en notion.so (free plan alcanza).
2. Pages base:
   - `Onboarding` — para cuando contrates primer VA.
   - `Runbooks` — procedimientos paso a paso.
   - `Weekly Notes` — journal de Javier.
3. En Paperclip → integrar Notion MCP (ya disponible).

---

## 18. Variables de entorno unificadas

Armar un archivo `.env.example` en el root del repo con todas las credenciales que los workflows necesitan. NO commitear el `.env` real — solo el `.example`.

```bash
# .env.example
# --- Google ---
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
# --- Slack ---
SLACK_BOT_TOKEN=xoxb-
SLACK_SIGNING_SECRET=
# --- HubSpot ---
HUBSPOT_API_KEY=
# --- Stripe ---
STRIPE_SECRET_KEY=sk_
STRIPE_WEBHOOK_SECRET=whsec_
# --- Supabase ---
SUPABASE_URL=
SUPABASE_SERVICE_ROLE=
SUPABASE_ANON=
# --- OpenAI / Anthropic ---
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
# --- Sales stack ---
INSTANTLY_API_KEY=
APOLLO_API_KEY=
CLAY_API_KEY=
APIFY_API_TOKEN=
HEYREACH_API_KEY=
FIREFLIES_API_TOKEN=
# --- n8n ---
N8N_WEBHOOK_BASE=https://n8n.jmconsulting.ai/webhook
```

---

## 19. Checklist final

Antes de cerrar: todo esto tiene que estar ✅:

- [ ] Paperclip: 6 agentes creados y respondiendo tests de humo.
- [ ] Gmail, Slack, CRM, Stripe: OAuth funcionando desde Paperclip y n8n.
- [ ] n8n: al menos JM-01, JM-02, JM-10 activos y testeados.
- [ ] Supabase: proyecto creado, 4 tablas base, credentials guardadas.
- [ ] 1Password: vault `JM-Consulting-Prod` con todos los secretos.
- [ ] Google Drive: estructura de folders + masters subidos.
- [ ] Fireflies: grabando calls automáticamente, JM-02 dispara en evento.
- [ ] Sales stack (Instantly + Apollo) activo si ya querés arrancar outbound.
- [ ] GitHub: repo inicial pusheado.
- [ ] Slack canales críticos creados (#heartbeat, #approvals, #alerts-prod, #alerts-cost, #pipeline).

---

## 20. Orden recomendado de go-live

**Día 1-2:** 1-Password + Gmail + Slack + Google Drive + Supabase + n8n cloud + CRM.
**Día 3:** Paperclip agentes conectados a todo lo anterior + tests de humo.
**Día 4-5:** Stripe + JM-06 + primeros 3 workflows JM (01, 02, 10).
**Semana 2:** Fireflies + JM-03 (onboarding) + JM-04 (MBR).
**Semana 3:** Sales stack (Instantly + Apollo + HeyReach) + warming + SE-01..04.
**Semana 4:** Clay (opcional) + SE-05..06 + primeros cold campaigns reales.

A partir de ahí: el OS ya está vivo. Los siguientes ciclos se hacen por iteración sobre workflows y agentes, no por setup.
