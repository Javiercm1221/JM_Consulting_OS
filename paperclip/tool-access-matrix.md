# Tool Access Matrix — Qué agente puede usar qué herramienta

Matriz de permisos por agente. Cada agente sólo accede a lo que necesita. Principio de menor privilegio.

## Leyenda

- ✅ — acceso completo (lectura y escritura).
- 👁 — solo lectura.
- 🔒 — acceso con approval humano previo.
- ❌ — sin acceso.

---

## Matriz principal

| Herramienta | CEO | CRO | Head Audit | CTO | COO | CMO | Client Success |
|---|---|---|---|---|---|---|---|
| **Paperclip (issues)** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Email outbound (Instantly)** | 👁 | ✅ | ❌ | ❌ | 👁 | ❌ | ❌ |
| **Email interno (Gmail)** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **CRM** | 👁 | ✅ | 👁 | ❌ | 👁 | ❌ | ✅ |
| **LinkedIn** | ❌ | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ |
| **Apollo / Clay** | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Calendly / Calendar** | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| **Fireflies / Otter** | 👁 | ✅ | ✅ | 👁 | ❌ | ❌ | ✅ |
| **Google Drive / Notion (docs)** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Slack (interno JM)** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Slack (compartido cliente)** | ✅ | 👁 | ✅ | ✅ | ❌ | ❌ | ✅ |
| **GitHub (código JM)** | 👁 | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **GitHub (código cliente)** | ❌ | ❌ | ❌ | 🔒 | ❌ | ❌ | ❌ |
| **n8n workflows JM** | 👁 | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| **n8n workflows cliente** | ❌ | ❌ | ❌ | 🔒 | ❌ | ❌ | 👁 |
| **LLM APIs (OpenAI, Anthropic)** | 👁 | ❌ | ✅ | ✅ | ❌ | ✅ | ❌ |
| **Supabase / DB cliente** | ❌ | ❌ | 👁 | 🔒 | ❌ | ❌ | ❌ |
| **1Password / Vault** | 👁 | ❌ | 🔒 | 🔒 | ✅ | ❌ | ❌ |
| **Stripe / billing** | 👁 | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Mercury / bank** | 👁 | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Contratos firmados** | 👁 | 👁 | 👁 | ❌ | ✅ | ❌ | 👁 |
| **Firma de contratos** | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Dashboards de clientes** | ✅ | 👁 | ✅ | ✅ | 👁 | ❌ | ✅ |
| **LinkedIn publishing** | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ |
| **Newsletter publishing** | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ |
| **Web landing** | ❌ | ❌ | ❌ | 🔒 | ❌ | ✅ | ❌ |

---

## Detalle de 🔒 (approvals requeridos)

### CTO → GitHub código cliente (🔒)
- Approval: Javier + account lead.
- Razón: código del cliente es propiedad / sensitivity alta.

### CTO → n8n workflows cliente (🔒)
- Approval: Javier.
- Razón: cambios en prod del cliente.

### CTO → Supabase / DB cliente (🔒)
- Approval: Javier + sponsor cliente.
- Razón: acceso a data productiva.

### Head of Audit / CTO → 1Password (🔒)
- Approval: COO.
- Razón: secrets críticos.

### CTO / CMO → Web landing (🔒 parcial)
- Approval: CMO para contenido, CTO para código.
- Razón: tech + contenido separados.

---

## Accesos que NADIE tiene (sólo Javier)

- Firma final de contratos legales.
- Decisiones sobre cambios de pricing base.
- Acceso a banco personal del fundador.
- Aprobación de gastos > 1K USD/mes nuevos.
- Alta / baja de agentes (nuevos roles).
- Cambio de stack core de la firma.

---

## Políticas transversales

### Credenciales
- Siempre vía vault (1Password / Bitwarden).
- Nunca en código.
- Nunca en prompts de LLM compartidos.
- Rotación cada 90 días para credenciales críticas.

### Data de clientes
- No se lee sin necesidad operativa.
- No se comparte entre agentes sin necesidad.
- Al terminar contrato, se archiva en read-only + purge programado si aplica.

### Logs de acceso
- Cada herramienta con logs de quién accedió qué.
- Auditoría trimestral de accesos por COO.

### Agentes Read-only por default
Cualquier agente nuevo se crea con accesos mínimos y se abren permisos con justificación y approval.

---

## Cuando un agente necesita acceso que no tiene

Flujo:
1. Agente detecta que necesita accesos.
2. Crea issue en Paperclip con "access request" + justificación.
3. Asigna al COO.
4. COO evalúa y escala a Javier si es 🔒.
5. Si se aprueba: COO otorga, agente retoma.
6. Si se rechaza: agente busca workaround.

---

## Revisión periódica

- COO revisa la matrix cada trimestre.
- Quita accesos de agentes que no los usaron en 90 días.
- Rota credenciales según política.
- Audita logs por anomalías.

---

## Ver también

- `/paperclip/approvals-policy.md`
- `/paperclip/ceo-instructions.md`
- Todos los `*-instructions.md`
