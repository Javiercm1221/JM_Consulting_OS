# Audit Deck — Outline del PPTX de cierre

Estructura del deck ejecutivo de 20-25 slides que cierra el audit. Este es **el activo que vende la implementación**.

## Objetivo

Que en 45 minutos el board o el comité directivo entienda:
1. Qué vimos (diagnóstico).
2. Cuánto vale arreglarlo (oportunidad).
3. Qué hacemos primero (plan).
4. Cuánto cuesta y cuánto rinde (inversión).

## Regla de oro

> Un slide = una idea = un número.

No meter 3 gráficos en un slide. No repetir números. Si un slide no tiene un número o una decisión, probablemente sobra.

---

## Estructura — 22 slides estándar

### Bloque 1 — Contexto (3 slides)

**Slide 1 — Portada**
```
AI Opportunity Audit — {{Company}}
Executive Deck · v1.0 · {{date}}
Javier Martinez — JM Consulting
```
Sobria. Logo de la empresa + logo JM.

**Slide 2 — Agenda**
- Contexto y outcomes (3 min).
- Business map (5 min).
- Oportunidades identificadas (15 min).
- Roadmap 90 días (10 min).
- Inversión y recomendación (7 min).
- Preguntas (5 min).

**Slide 3 — Outcomes aprobados**
Tabla con los 3-5 outcomes definidos en el paso 1 del framework.
Baseline / Target / Sponsor.

---

### Bloque 2 — Diagnóstico (5 slides)

**Slide 4 — Business map**
Diagrama visual de las 4 zonas (Adq / Ent / Ret / Back).
Anotar dónde están los handoffs críticos con puntos rojos.

**Slide 5 — Cómo trabajamos: metodología**
6 pasos del framework en una línea horizontal.
Marcar tiempo dedicado a cada uno.

**Slide 6 — Lo que escuchamos**
3-5 quotes literales de entrevistas (anonimizados o con nombre según NDA).
Subrayar la emoción del quote, no la estadística.

**Slide 7 — Tareas mapeadas**
Número total: "{{N}} tareas, {{X}} horas/sem, USD {{Y}}/año en costo humano directo".
Visual: bar chart de top 10 tareas por costo anual.

**Slide 8 — Dónde está la fuga**
Visual: heatmap de las 4 zonas coloreado por dólares/año.
"El 68% del costo operativo capturado está en {{zona}}".

---

### Bloque 3 — Oportunidades (6 slides)

**Slide 9 — Filtro de feasibility**
Las 4 preguntas del filtro IA.
"{{X}} tareas pasaron el filtro de 4/4, {{Y}} de 3/4."

**Slide 10 — Opportunity matrix**
Gráfico 2D (impacto × effort). Puntos nombrados.
Marcar los 3 quick wins con estrella.

**Slide 11 — Oportunidad #1 (Quick win)**
- Nombre y 1 frase de descripción.
- Beneficio anual: USD {{}}.
- Effort: {{semanas}}.
- Payback: {{meses}}.
- Stack: {{tecnología}}.
- Quote apoyo: "{{lo que dijo el operador}}".

**Slide 12 — Oportunidad #2 (Quick win)**
Misma estructura.

**Slide 13 — Oportunidad #3 (Quick win)**
Misma estructura.

**Slide 14 — Big swing(s)**
1-2 oportunidades de mayor impacto/effort. Misma estructura pero con nota "planificar Q2".

---

### Bloque 4 — Plan (4 slides)

**Slide 15 — Roadmap 90 días (Gantt)**
Visual Gantt por semana. Colorear por tipo (quick win / big swing).

**Slide 16 — Recursos y owners**
Tabla: actividad | owner JM | owner cliente | horas estimadas cliente.

**Slide 17 — Quick wins esperados (mes 1-3)**
3 bullets grandes con el resultado esperado al final del trimestre:
- Lead response < 5 min (desde 3h).
- 70% tickets clasificados automáticamente.
- Reportes semanales automatizados.

**Slide 18 — Riesgos y mitigaciones**
Tabla top 5 riesgos: descripción | probabilidad | impacto | mitigación.

---

### Bloque 5 — Inversión (3 slides)

**Slide 19 — ROI consolidado**
Tabla grande:
| Quick wins | Big swings | Total Año 1 |
| Beneficio | | | |
| Costo | | | |
| ROI | | | |
| Payback | | | |

Nota al pie: "Supuestos: ver ROI Calculator adjunto."

**Slide 20 — Opciones comerciales**
Tres opciones presentadas lado a lado:

| Opción A | Opción B | Opción C |
|---|---|---|
| Solo Quick Wins | Quick Wins + Big Swing 1 | Full Roadmap |
| USD {{}} | USD {{}} | USD {{}} |
| Payback X | Payback X | Payback X |
| Start: {{fecha}} | Start: {{fecha}} | Start: {{fecha}} |

**Slide 21 — Recomendación**
Opción B (la del medio) en grande. "Balance óptimo de impacto y velocidad."
Incluir:
- Próximos pasos (firma, kickoff).
- Equipo JM asignado con nombres/fotos.
- Credit del audit (100% aplicado).

---

### Bloque 6 — Cierre (1 slide)

**Slide 22 — Preguntas / contacto**
Email, Slack, calendar link.
QR a la propuesta formal.

---

## Opcionales (slides adicionales si hacen falta)

- **Caso de estudio similar** (antes/después de otro cliente).
- **Comparación con competidores en tecnología adoptada.**
- **Testimonios** (si hay NDA que lo permita).
- **FAQ** (preguntas típicas del board).

---

## Reglas de diseño

### Tipografía
- Headers: sans-serif bold, 28-36pt.
- Body: sans-serif regular, 18-22pt.
- Números grandes: 48-72pt en los slides clave.

### Paleta
- Principal: azul corporativo JM (#0F3B66) + blanco.
- Acento: verde (#2EA86E) para positivos, rojo (#D64545) para negativos.
- Neutros: gris oscuro (#2D3339), gris claro (#EDEFF2).

### Imágenes / íconos
- Íconos Lucide / Feather.
- Gráficos: matplotlib o Chart.js exportados a PNG.
- Sin stock photos clichés.

### Números
- USD con separador de miles (1,245,000).
- Porcentajes con 0 o 1 decimales (67.4%).
- Horas redondeadas a enteros arriba de 10 (15 h vs 15.3).

---

## Revisión pre-entrega

Antes de presentar:
- [ ] Todos los números consistentes con el ROI Calculator.
- [ ] Cada quote anonimizado o autorizado.
- [ ] Logos y nombres de empresa correctos (typos matan credibilidad).
- [ ] Revisar en modo presentación real, no solo en edición.
- [ ] Backup en PDF.
- [ ] Backup en imprenta (PDF horizontal 11×17 si se quiere handout).

---

## Post-presentación

- [ ] Enviar deck final en < 24 h.
- [ ] Enviar ROI Calculator editable con password compartido.
- [ ] Enviar propuesta formal en < 48 h.
- [ ] Agendar call de follow-up a 7-10 días.
- [ ] Cargar en CRM: stage "audit presented → proposal sent".

---

## Variables estándar del deck

Mantener un JSON con las variables que se reemplazan por cliente:

```json
{
  "company": "",
  "sponsor_name": "",
  "sponsor_role": "",
  "audit_date": "",
  "industry": "",
  "employees": 0,
  "outcomes": [],
  "opportunities": [],
  "investment_options": {
    "A": {"cost": 0, "payback": 0},
    "B": {"cost": 0, "payback": 0},
    "C": {"cost": 0, "payback": 0}
  }
}
```

---

## Template maestro

El archivo físico en blanco vive en `/assets/deck/JM_Audit_Deck_MASTER.pptx`.

Ver también el skill `pptx` cuando se genere la versión física del template.

## Referencias

- Paso previo: `/audit/roi-calculator-spec.md`
- Framework: `/audit/roi-first-framework.md`
- Propuesta comercial: `/assets/proposals/audit_proposal_template.docx` (en backlog)
