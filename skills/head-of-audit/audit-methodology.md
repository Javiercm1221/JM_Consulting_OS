# Audit Methodology — 10 días hábiles

## Cronograma estándar

```
Día 1  | Kickoff + outcomes session con sponsor (60 min)
Día 2  | Primera entrevista stakeholder (1–2 ejecutivos)
Día 3  | Entrevistas stakeholders (2–3) + planificación operadores
Día 4  | Entrevistas operadores (2–3) — arranque Yesterday Morning
Día 5  | Entrevistas operadores (2–3) + observación directa
Día 6  | Business map v1 + revisión con sponsor (60 min)
Día 7  | Task map completo + filtro AI feasibility
Día 8  | Opportunity matrix + ROI calculator v1
Día 9  | Deck ejecutivo armado (review interno JM)
Día 10 | Presentación al sponsor (90 min) + entregables finales
```

Buffer: 2–3 días adicionales opcionales para reajustes sin costo.

## Paso 1 — Outcomes session (Día 1)

Objetivo: acordar por escrito qué define el éxito del audit.

Preguntas clave:
- "Si en 10 días terminamos el audit y está todo bien hecho, ¿qué tres cosas querría ver en el deck?"
- "¿Cuál es el proceso más caro o lento en su empresa hoy?"
- "¿Qué decisiones necesita poder tomar con los outputs del audit?"

Output: documento de outcomes firmado digitalmente por el sponsor.

## Paso 2 — Business Map (Días 2–6)

Mapear los procesos de negocio a alto nivel:
- ¿Qué departamentos/áreas existen?
- ¿Cómo fluye el trabajo entre ellas?
- ¿Dónde están los handoffs manuales?
- ¿Dónde se pierde información?

Herramientas: Excalidraw, Miro, o simplemente papel + foto.
Validar con el sponsor en Día 6 antes de bajar al task map.

## Paso 3 — Task Map (Día 7)

Para cada proceso del business map, descomponer en micro-tareas:
- Nombre de la tarea
- Quién la hace
- Frecuencia (diaria / semanal / por evento)
- Tiempo promedio (minutos)
- Herramientas usadas
- Fuente de error / cuello de botella
- Costo estimado (tiempo × salario)

Formato: Google Sheets / Excel con una fila por micro-tarea.

Mínimo: 30–50 micro-tareas para un audit completo.

## Paso 4 — AI Feasibility Filter (Día 7)

Para cada micro-tarea, aplicar el filtro de 4 preguntas:

1. **¿Es repetitiva?** — ¿Pasa > 10 veces por semana?
2. **¿Tiene input estructurado o estructurable?** — ¿Se puede definir claramente qué entra?
3. **¿El output es verificable?** — ¿Se puede saber si la IA lo hizo bien?
4. **¿El costo de error es bajo o mitigable?** — ¿Hay humano en el loop disponible?

4/4 → Alta candidatura para IA
3/4 → Media, depende del costo de error
< 3/4 → No automatizar ahora

## Paso 5 — Opportunity Matrix (Día 8)

Para cada tarea que pasó el filtro de feasibility:

| Campo | Descripción |
|---|---|
| Nombre de la oportunidad | Nombre corto y descriptivo |
| Proceso fuente | De dónde viene en el task map |
| ROI anual estimado (USD) | Ahorro + revenue generado |
| Haircut (–20%) | Proyección conservadora |
| Esfuerzo de implementación | Semanas + costo estimado |
| ROI / Esfuerzo ratio | Prioridad |
| Dependencias | Qué necesita para funcionar |
| Riesgo principal | Qué puede salir mal |

Ordenar por ROI/Esfuerzo ratio de mayor a menor.
Los top 3 son los "Quick Wins" recomendados.

## Paso 6 — ROI Calculator (Día 8)

Usar `ROI_Calculator_MASTER.xlsx`:
1. Ingresar supuestos del cliente en sheet "Supuestos".
2. El dashboard recalcula automáticamente.
3. Capturar screenshot del dashboard para el deck.

Fórmula base:
```
ROI = (Ahorro anual + Revenue incremental) / Costo de implementación
Payback = Costo de implementación / (Ahorro mensual + Revenue mensual)
```

Siempre aplicar haircut del 20% a las proyecciones antes de presentar.

## Paso 7 — Deck ejecutivo (Días 9–10)

Estructura del deck (usar `Audit_Deck_MASTER.pptx`):

1. Portada + agenda
2. Resumen ejecutivo (3 bullets)
3. Business map (visual)
4. Top 3 oportunidades con ROI
5. Opportunity matrix completa
6. Roadmap 90 días
7. Inversión requerida (Quick Wins Sprint)
8. Próximos pasos + propuesta de implementación

El deck NO incluye precio de implementación — eso va en la propuesta separada que maneja el CRO.
