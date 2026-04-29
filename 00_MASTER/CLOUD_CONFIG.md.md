---
type: config
version: 1.0
---

# 🤖 CLOUD_CONFIG — Claude en Cowork

## Instrucciones para Claude

Cuando Javier (en Cowork) adjunta su vault y pide actualización:

### 1. Lee primero
- `/00_MASTER/INDEX.md` (estructura y qué contiene cada carpeta)
- Este archivo (CLOUD_CONFIG.md)

### 2. Entiendes que tienes estas carpetas:

/company → Misión, positioning, pricing 
/sales → Clientes, outbound, scripts 
/audit → ROI framework, entrevistas 
/delivery → Implementación, QA 
/maintenance → Retainer, soporte 
/paperclip → Roles, issues, heartbeat 
/n8n → Workflows 
/assets → Decks, propuestas, case studies 
/client_pods_template → Template por cliente 
/guides → Guías de setup

### 3. Cuando Javier pide INGEST (nuevo cliente/dato)
- Identificas dónde va (probablemente `/sales` para cliente, `/delivery` para proyecto)
- Creas archivo con estructura simple:
  - Título: # [Nombre]
  - Metadata: tipo, fecha, links relacionados
  - Contenido: breve, claro, Markdown
- Actualizar INDEX.md si es relevante
- Devuelves vault

### 4. Cuando Javier pide QUERY (pregunta)
- Lees su INDEX.md
- Navegas a carpetas relevantes
- Respondes con datos
- No modificas Obsidian

### 5. Cuando Javier pide SYNC-METRICS
- Lees `/sales` (clientes)
- Recalculas conversión, ROI
- Actualiza INDEX.md con nuevos números
- Devuelves vault

### 6. Cuando Javier pide AUDIT
- Validas que archivos tengan:
  - Título
  - Contenido básico
  - Enlaces relacionados si aplica
- Reportas qué arreglar
- No modificas, solo reporta

## Variables de Contexto
- Empresa: JM Consulting
- Servicios: AI Audit, Lead Gen, Quick Wins, Implementation, Retainer
- Mercado: Startups, SMEs en Europa
- Stack: Apify, Airtable, n8n, Instantly.ai

## Regla Más Importante
**Nunca crear carpetas nuevas.** Solo usar las que existen. Al menos que sea realmente importante y con permiso mediante. 