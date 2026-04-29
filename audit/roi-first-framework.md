# Framework de Auditoría ROI-First

La metodología nuclear de JM Consulting. **Todo lo que vende y todo lo que entrega se para sobre este framework.**

## Filosofía

> Primero el dinero, después la tecnología. La IA no es el producto — el ROI sí lo es.

Regla operativa: ningún cliente contrata implementación sin haber pasado por el audit. Ningún audit entrega recomendaciones sin un número en dólares al lado de cada una.

## Los 6 pasos

```
1. Outcomes  →  2. Business Map  →  3. Task Map  →
4. AI Feasibility  →  5. Opportunity Matrix  →  6. ROI
```

Cada paso tiene inputs, outputs y checkpoints. No se salta ningún paso.

---

## Paso 1 — Outcomes (Día 1-2)

### Objetivo
Definir qué resultados empresariales quiere el sponsor ejecutivo en 12 meses. Sin esto, el audit termina siendo "IA genérica".

### Inputs
- Reunión con CEO / COO / Managing Partner.
- P&L resumido (o rangos).
- Plan anual / OKRs vigentes.

### Outputs
- Lista priorizada de 3-5 outcomes medibles.
- Cada uno con métrica, baseline actual, target a 12 meses, responsable.

### Template de outcomes
```
| Outcome | Métrica | Baseline | Target 12m | Sponsor |
|---|---|---|---|---|
| Crecer revenue sin agrandar equipo | MRR / headcount | 8K/FTE | 14K/FTE | CEO |
| Bajar tiempo de respuesta a leads | Time-to-first-touch | 3h | <5min | Sales Lead |
| Reducir costo de back-office | Horas admin / unidad | 2.1h | 1.0h | COO |
```

### Preguntas guía
1. ¿Qué métrica de negocio tiene que cambiar en 12 meses para que esto haya sido un éxito?
2. ¿Dónde perdés dinero y ya lo sabés, pero no te da tiempo de arreglarlo?
3. ¿Qué cosa te haría decir "esto fue lo mejor que hicimos este año"?
4. ¿Si tuvieras 3× el equipo, qué harías primero?

### Checkpoint
Antes de pasar al paso 2, el sponsor tiene que poder decir en una frase qué significa éxito. Si no puede, el audit se queda acá.

---

## Paso 2 — Business Map (Día 2-4)

### Objetivo
Mapear la empresa como **sistema de flujos de valor**, no como un organigrama.

### Inputs
- Entrevistas con líderes de área (30-45 min c/u).
- Documentación operativa existente.
- Stack tecnológico.

### Outputs
- Business map: áreas, procesos, flujos entre áreas, stack.
- Diagrama visual (Excalidraw / Miro / Paperclip canvas).

### Estructura del business map

```
┌─────────────────────────────────────────────────┐
│              Cliente / Usuario                   │
└────────────────┬────────────────────────────────┘
                 │
        ┌────────▼────────┐
        │   Adquisición   │  ← Marketing · Sales · Partnerships
        └────────┬────────┘
                 │
        ┌────────▼────────┐
        │   Entrega       │  ← Onboarding · Ops · Fulfillment
        └────────┬────────┘
                 │
        ┌────────▼────────┐
        │   Retención     │  ← Support · Success · CSM
        └────────┬────────┘
                 │
        ┌────────▼────────┐
        │   Back-office   │  ← Finanzas · HR · Legal · Compliance
        └─────────────────┘
```

Cada bloque:
- Procesos clave.
- Sistemas / software usados.
- Personas clave.
- KPIs que miden.
- Dolor reportado.

### Checkpoint
El sponsor tiene que decir "sí, así es mi empresa" al ver el mapa. Si no, ajustar antes de avanzar.

---

## Paso 3 — Task Map (Día 4-7)

### Objetivo
Descomponer cada proceso en **tareas concretas, cuantificadas en horas y dinero**.

### Inputs
- Entrevistas 1-a-1 con ejecutores (empleados de cada proceso).
- Observación directa cuando sea posible (shadowing).
- Logs de sistemas (tickets, CRM, support).

### Método de entrevista — Yesterday Morning

> "Contame qué hiciste ayer a la mañana. ¿Qué fue lo primero? ¿Después? ¿Después?"

Esta técnica revela:
- Pasos ocultos que nadie documenta.
- Re-trabajo invisible.
- Handoffs lentos.
- Tareas repetitivas no reconocidas.

### Plantilla de task map (un renglón por tarea)

```
| Task | Proceso | Frecuencia | Tiempo/vez | Volumen/sem | Personas | Costo/hora | Costo/sem |
|---|---|---|---|---|---|---|---|
| Responder lead web | Adquisición | Por lead | 8 min | 140 | 2 | $25 | $467 |
| Armar PMS ticket | Ops | Por incidencia | 12 min | 80 | 3 | $22 | $352 |
| Reconciliar banco | Finanzas | Semanal | 180 min | 1 | 1 | $35 | $105 |
```

### Reglas de captura
- Si una tarea consume > 2 h/semana a alguien, se mapea.
- Si un proceso toca > 3 personas, se mapea cada handoff.
- Si algo sucede > 20 veces/semana, se cuenta aunque sean segundos.

### Checkpoint
Tener **≥ 40 tareas** mapeadas para una empresa mediana. Si hay menos, seguir entrevistando.

---

## Paso 4 — AI Feasibility (Día 7-9)

### Objetivo
Filtrar task por task: **¿esto se automatiza con IA, con automation clásica, o no se toca?**

### Filtro de 4 preguntas

Aplicar a cada tarea:

```
1. ¿Input estructurado o estructurable?        [sí / no]
2. ¿Output predecible / plantillable?          [sí / no]
3. ¿Decisión sigue reglas documentables?       [sí / no]
4. ¿Se repite con frecuencia alta?             [sí / no]
```

| Sí's | Recomendación |
|---|---|
| 4 | IA rinde — candidato fuerte |
| 3 | IA + humano en loop |
| 2 | Automation simple (n8n, Zapier, scripts) |
| 1 | Mejorar proceso antes de automatizar |
| 0 | Dejar manual / rediseñar |

### Clasificación adicional
Cada task candidata se etiqueta:

- **Tipo de solución**: RAG, agente, clasificación, extracción, generación, workflow automation.
- **Sensibilidad de datos**: pública, interna, confidencial, regulada.
- **Integración necesaria**: API, webhook, DB, email, chat.

### Checkpoint
Lista de 15-30 candidatas pasando el filtro, con tipo de solución identificado.

---

## Paso 5 — Opportunity Matrix (Día 9-11)

### Objetivo
Priorizar: de las 15-30 candidatas, ¿cuáles arrancamos primero?

### Ejes

```
                  Impacto económico (USD/año)
                          ↑
                          │
         Big swings       │    Quick wins  ⭐ PRIORIDAD 1
         (planificar)     │    (ejecutar ya)
                          │
──────────────────────────┼──────────────────────────→
                          │                    Effort (semanas)
         Deprioritize     │    Nice-to-haves
         (no tocar)       │    (backlog)
                          │
```

### Cálculo de impacto
```
Impacto = (horas_ahorradas × costo_hora × 52) + (revenue_recuperado) − (costo_solución)
```

### Cálculo de effort
```
Effort = semanas_implementación + complejidad_integración + cambio_proceso_humano
```
Escala 1-5.

### Plantilla de matrix (output)

```
| # | Oportunidad | Impacto $/año | Effort | Cuadrante | Owner |
|---|---|---|---|---|---|
| 1 | Auto-respuesta leads web | 180K | 2 | Quick win | Sales Lead |
| 2 | IA draft de contratos | 320K | 4 | Big swing | Legal |
| 3 | Bot QA interno | 40K | 1 | Quick win | Ops |
| 4 | RAG manual empleados | 25K | 3 | Nice-to-have | HR |
```

### Checkpoint
**Top 10 oportunidades ranked, 3-5 en cuadrante Quick Win.**

---

## Paso 6 — ROI + Roadmap (Día 11-14)

### Objetivo
Entregar **números, no diapositivas**. Cada oportunidad con payback calculado y fecha.

### Fórmula base del ROI

```
ROI anual = (Ahorro_anual + Revenue_incremental − Costo_total) / Costo_total

Payback (meses) = Costo_total / (Beneficio_mensual)
```

### Componentes de Costo_total
- Costo de modelos IA (tokens, inference).
- Costo de infra (cloud, vector DB).
- Costo de implementación (horas JM Consulting × rate).
- Costo de mantenimiento (retainer o horas).
- Costo de cambio operativo (training, tiempo del equipo).

### Roadmap 90 días

```
| Semana | Entregable | Owner JM | Owner Cliente | Depende de |
|---|---|---|---|---|
| 1 | Kickoff + accesos | PM | Sponsor | - |
| 2 | Workflow 1 piloto (auto-respuesta leads) | CTO | Sales Lead | Datos CRM |
| 3 | Workflow 1 en producción | CTO | Sales Lead | Semana 2 |
| 4 | Medir lift vs baseline | PM | Sales Lead | Semana 3 |
| 5-7 | Workflow 2 (QA bot) | CTO | Ops Lead | - |
| 8-12 | Workflow 3 (contratos) | CTO + Legal | Legal Lead | Semana 7 |
```

### Deck ejecutivo — outline
Ver `/audit/audit-deck-outline.md`. Secciones:
1. Contexto y outcomes.
2. Business & task map.
3. Opportunity matrix (visual).
4. Top 10 con ROI.
5. Roadmap 90 días.
6. Inversión y recomendación.

### Checkpoint
Sponsor firma el roadmap o pide iteración. Si lo firma, pasa a `/delivery`.

---

## Tiempo total del audit

| Día | Actividad | Entregable |
|---|---|---|
| 1-2 | Outcomes + kickoff | Doc outcomes firmado |
| 3-7 | Entrevistas (5-10) | Business map + task map |
| 8-9 | Feasibility | Lista de candidatas |
| 10-11 | Opportunity matrix | Matrix priorizada |
| 12-13 | ROI + roadmap | ROI calculator poblado + roadmap |
| 14 | Presentación | Deck + sesión 90 min con sponsor |

**Total: 10 días hábiles + buffer.**

---

## Entregables finales del audit

Al cierre, el cliente recibe:

1. **Executive Deck** (20-25 slides, PPTX/Keynote).
2. **ROI Calculator** (XLSX interactivo por oportunidad).
3. **Business Map** (diagrama visual).
4. **Task Map** (tabla extensa, XLSX).
5. **Opportunity Matrix** (visual + ranking).
6. **Roadmap 90 días** (Gantt simple).
7. **Propuesta de implementación** (DOCX, opcional, si hay go).
8. **Sesión ejecutiva** (90 min, grabada).

---

## Pricing del audit

- **Estándar:** 10K USD flat.
- **Large enterprise (>500 empleados o >50M USD rev):** 20-50K USD.
- **Crediting:** 100% del audit se acredita a la primera implementación dentro de 90 días.
- **Garantía:** si no identificamos fugas por al menos 3× el costo del audit, devolvemos el 50%.

---

## Reglas innegociables

1. **Nunca recomendar IA donde no aplica.** Decir "esto es automation simple" y cobrar menos genera más confianza que meter IA de adorno.
2. **Nunca entregar sin número.** Cada oportunidad con USD/año, effort, payback.
3. **Nunca saltarse outcomes.** Sin outcomes firmados, no hay paso 2.
4. **Nunca presentar sin validar con operadores.** Si el equipo que ejecuta no vio el task map, no se presenta.
5. **Nunca mover deliverables a más de 14 días hábiles.** Audit que se dilata pierde momentum y cierre.

---

## Referencias

- `/audit/outcome-definition.md` — plantilla paso 1
- `/audit/stakeholder-interviews.md` — plantillas ejecutivos
- `/audit/employee-interviews.md` — plantillas operadores
- `/audit/yesterday-morning-method.md` — técnica de descubrimiento
- `/audit/business-map-template.md` — plantilla paso 2
- `/audit/task-map-template.md` — plantilla paso 3
- `/audit/opportunity-matrix.md` — plantilla paso 5
- `/audit/roi-calculator-spec.md` — especificación del XLSX
- `/audit/audit-deck-outline.md` — estructura del PPT final
