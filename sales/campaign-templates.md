# Campaign Templates — Campañas completas por nicho

Plantillas de campañas end-to-end por vertical. Cada plantilla contiene: **ICP target / canal / cadencia / copy / CTA / KPI**.

Variables estándar: `{{firstName}}`, `{{lastName}}`, `{{company}}`, `{{city}}`, `{{role}}`, `{{numberEmployees}}`, `{{painPoint}}`, `{{triggerObserved}}`, `{{competitor}}`, `{{industry}}`, `{{practiceArea}}`, `{{calendarLink}}`.

---

## Framework de personalización (aplica a toda campaña)

Toda primera línea debe contener al menos **1 dato verificable** del prospecto. Fuentes:

- LinkedIn post reciente (< 14 días).
- Note de prensa de la empresa.
- Job posting activo.
- Review pública reciente (Google, Trustpilot).
- Cambio de web / landing nuevo.
- Evento sectorial en el que participó.

Regla: si no hay data para personalizar, **no enviar**. Mejor no tocar al lead que quemar el dominio.

---

## Campaña 1 — Property Management (EEUU/LATAM)

### ICP target
Firmas de 100-2.000 unidades gestionadas, 20-150 empleados, uso de AppFolio / Buildium / Yardi. Decisor: COO / Director of Operations.

### Canal principal
Email outbound (4 toques) + LinkedIn (manual, 2 toques).

### Cadencia
- Día 0: Email 1.
- Día 3: Email 2.
- Día 5: LinkedIn connection request.
- Día 7: Email 3 (oferta audit).
- Día 10: LinkedIn mensaje si aceptó.
- Día 14: Email 4 (breakup).

### Subject lines (test A/B)
1. `{{firstName}}, pregunta sobre {{company}}`
2. `Lead response en {{company}}`
3. `{{city}} property ops — 3 quick wins`
4. `{{firstName}} — 100K fuga silenciosa`

### Email 1 — gancho
```
Hola {{firstName}},

Vi que {{company}} gestiona ~{{numberEmployees}} unidades en {{city}}.
En firmas de property mgmt de ese tamaño encontramos que el lead response
(habitualmente 3-4 h) y la coordinación de mantenimiento son las dos fugas
más caras —algunos clientes perdían 100K+/año sin verlo.

¿Te mando los 3 quick wins más comunes en firmas similares? Te lo paso
en 2 párrafos, sin agenda.

— Javier · JM Consulting
```

### Email 2 — prueba social (día 3)
```
{{firstName}},

Mientras te armo los quick wins, un dato: un cliente en Orlando bajó
lead response de 4 h a <5 min y subió conversión de tours +4 puntos.
Implementación 5 semanas, payback 2 meses.

¿20 min esta semana? Te muestro el mapa y vemos si aplica a {{company}}.
```

### Email 3 — oferta audit (día 7)
```
{{firstName}},

Te cuento el formato que uso: una auditoría ROI-first de 2 semanas.
5-10 entrevistas con tu equipo, mapa completo de procesos, top 5-10
oportunidades de IA con ROI calculado, roadmap 90 días con quick wins
primero, y deck ejecutivo.

Pricing: 10K USD flat. Si contratás implementación, el 100% se
acredita al proyecto.

¿Agendamos 20 min? {{calendarLink}}
```

### Email 4 — breakup (día 14)
```
{{firstName}}, cierro el hilo. Si en los próximos 6 meses querés
mirar dónde fuga plata tu operación, el link sigue abierto.

Éxitos con {{company}}. — Javier
```

### KPI target
- Open > 55%, reply > 4%, positive > 2%, meetings booked / 100 leads > 1.5.

---

## Campaña 2 — Accounting / Bookkeeping

### ICP target
Firmas CPA/contables 10-80 personas, facturación 1-15M USD, stack moderno (QuickBooks Online, Xero, Dext). Decisor: Managing Partner / COO.

### Canal principal
Email + LinkedIn. Timing: post-tax-season (mayo-junio) y Q4.

### Subject lines
1. `{{firstName}}, post-tax season en {{company}}`
2. `Data entry en {{company}} — 60% descargable`
3. `Reconciliación automática en firmas como {{company}}`

### Email 1
```
{{firstName}},

En firmas de accounting del tamaño de {{company}} el dolor recurrente es
que el equipo senior se atasca en data entry y reconciliación que podrían
descargarse en 60-70% con IA aplicada a documentos.

¿Les pasa? Si sí, tengo un framework de auditoría de 2 semanas que
pone la fuga en dólares antes de proponer tecnología.

¿20 min esta semana?
```

### Email 2 — caso
```
{{firstName}}, un cliente CPA de 40 personas en Monterrey bajó horas
de reconciliación de 320/mes a 90 con un workflow de IA + Dext.
Payback 3 meses.

Te cuento el framework en 20 min. {{calendarLink}}
```

### Email 3 — oferta
```
{{firstName}}, el audit ROI-first que uso identifica las 5-10
oportunidades con más upside en tu firma en 2 semanas. 10K flat,
acreditable 100% si después implementamos.

¿Agendamos?
```

### KPI target
- Open > 50%, reply > 3.5%, meetings / 100 > 1.

---

## Campaña 3 — Legal boutique

### ICP target
Estudios boutique 5-40 abogados, practice areas: corporate, immigration, real estate, family, IP. Decisor: Managing Partner.

### Canal principal
Email + LinkedIn (el canal LinkedIn rinde más en legal).

### Subject lines
1. `{{firstName}}, intake en {{company}}`
2. `Draft automático en {{practiceArea}}`
3. `Discovery docs en {{company}}`

### Email 1
```
{{firstName}},

Vi que {{company}} trabaja {{practiceArea}}. En estudios boutique
de tu tamaño encontramos siempre dos fugas grandes: intake lento
(horas a días) y armado repetitivo de documentos.

Una auditoría de 2 semanas pone números a cada uno y propone
quick wins antes de tocar tecnología. ¿Tiene sentido 20 min?
```

### Email 2 — prueba social
```
{{firstName}}, un estudio de immigration en Miami bajó tiempo de
intake de 48 h a 2 h con un workflow IA + calendario. 120 leads/mes
ahora procesables vs 60. Payback 4 meses.

¿Agendamos 20 min para revisar tu caso?
```

### Email 3 — oferta audit
```
{{firstName}}, el audit ROI-first que hago es 10K flat, 2 semanas,
con NDA desde el día 0 (crítico en legal).

Entregables: mapa de procesos, 5-10 oportunidades, ROI, roadmap
y deck. 100% acreditable si implementamos.

{{calendarLink}}
```

### KPI target
- Open > 50%, reply > 4%, meetings / 100 > 1.2.

---

## Campaña 4 — Logística / 3PL

### ICP target
Operadores logísticos 50-500 personas, con TMS/WMS moderno. Decisor: COO / Director of Operations.

### Email 1
```
{{firstName}}, en 3PL/logística del tamaño de {{company}} las dos
fugas más caras suelen ser: tracking manual de cargas y respuesta
a consultas de clientes sobre status. Ambas descargables en gran
parte con IA + automation.

Una auditoría de 2 semanas te da números concretos. ¿20 min?
```

### KPI target
- Open > 50%, reply > 3%, meetings / 100 > 1.

---

## Campaña 5 — Healthcare no-crítica (clínicas, dental, estética)

### ICP target
Clínicas multi-sede, 10-100 empleados, stack con EHR moderno. Decisor: Director / Owner.

### Email 1
```
{{firstName}},

En clínicas como {{company}} el churn de pacientes que no vuelven
y la respuesta lenta a consultas por WhatsApp suelen ser las dos
fugas más caras. Ambas recuperables con workflows de IA + CRM.

Tengo un framework de auditoría de 2 semanas que cuantifica la
fuga antes de proponer nada. ¿20 min?
```

### KPI target
- Open > 50%, reply > 3%.

---

## Campaña 6 — B2B SaaS (post-product-market-fit)

### ICP target
SaaS series A-B, 30-200 personas. Decisor: VP Ops / VP CS / CTO.

### Email 1
```
{{firstName}}, vi que {{company}} acaba de cerrar {{triggerObserved}}.
En SaaS post-PMF el talón de aquiles son los procesos internos
(onboarding, support tiering, churn analytics) que quedaron pegados
con tape.

Hacemos audit ROI-first de 2 semanas. ¿20 min?
```

### KPI target
- Open > 55% (SaaS responde más), reply > 4%.

---

## Calendar & triggers estacionales

| Vertical | Ventanas | Trigger |
|---|---|---|
| Property Mgmt | Enero, abril, septiembre | Budget anual, post Q1, plan operativo |
| Accounting | Mayo, octubre, enero | Post-tax season, plan fiscal, presupuesto |
| Legal | Enero, septiembre | Plan anual, back-from-summer |
| Logística | Marzo, octubre | Preparación peak season, post-peak |
| Healthcare | Febrero, septiembre | Post-holidays, back-to-school |
| SaaS | Enero, julio | Planning anual, mid-year review |

---

## CTA library (por etapa del funnel)

**Top-of-funnel (curiosidad):**
- ¿Te mando los 3 quick wins más comunes en firmas similares?
- ¿Te interesa ver el framework? (link PDF)
- ¿Querés que te comparta el caso en 2 párrafos?

**Middle (engagement):**
- ¿20 min esta semana para mapear tu caso?
- ¿Agendamos 25 min el {{day}} para revisar la operación?
- ¿Te armo el one-pager para tu equipo?

**Bottom (cierre):**
- ¿Arrancamos con el audit? {{calendarLink}}
- Propuesta en tu inbox en 24 h + dos fechas de kickoff.
- ¿Quién más tiene que ver esto para aprobarlo?

---

## Subject lines — banco maestro (testeado)

**Gancho directo:**
- `{{firstName}}, pregunta sobre {{company}}`
- `2 min sobre ops de {{company}}`
- `{{company}} — fuga silenciosa`

**Dolor-driven:**
- `Lead response en {{company}}`
- `Data entry en {{company}}`
- `{{painPoint}} en {{company}}`

**Curiosidad / número:**
- `100K en {{city}}`
- `60% descargable`
- `3 quick wins para {{company}}`

**Referencial:**
- `Cliente similar a {{company}} (Orlando)`
- `{{competitor}} hizo esto, pensé en {{company}}`

Regla: < 7 palabras, primera letra del primer nombre minúscula si viene en saludo — salvo subject.

---

## Follow-up rules

- Esperar **48 h mínimo** entre toques de email.
- **Nunca hacer 3 toques el mismo día** (email + linkedin + call → spam flag).
- Si abre 2+ veces el mismo email → llamar manualmente.
- Si hay reply positivo → contestar en **< 60 minutos**.
- Si hay reply negativo → agradecer y pedir permiso para retomar en 90 días.
- Breakup siempre incluye "éxitos con {{company}}" (no dejar puerta cerrada).

---

## A/B testing plan

Cada 100 leads testear **una variable por vez**:

- Subject (2 versiones).
- Primera línea (dato de empresa vs dato de persona).
- Largo (60 palabras vs 120).
- CTA (calendario directo vs pregunta abierta).

Nunca cambiar 2 variables al mismo tiempo — no se aprende.

---

## Logging por campaña

Cada campaña se carga en el tracker (Airtable/Sheets) con:

```
campaign_id | vertical | canal | start_date | leads_total | sent | opens | replies | positives | meetings | deals | notes
```

Revisión semanal el viernes. KPIs que bajan 2 semanas seguidas → pausar campaña y rotar copy.

---

## Referencias cruzadas

- `/sales/offer-scripts.md` — copy base por canal
- `/sales/discovery-call-script.md` — script post-reply positivo
- `/sales/objection-handling.md` — banco de respuestas
- `/sales/niches.md` — selección de vertical y timing
- `/sales/outbound-playbooks.md` — stack técnico por canal
