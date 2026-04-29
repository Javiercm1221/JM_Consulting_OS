# Opportunity Matrix — Paso 5 del audit

Priorización visual de las oportunidades detectadas. Input para el roadmap de 90 días.

## Filosofía

> No ganamos por hacer muchas cosas. Ganamos por hacer la cosa correcta primero.

La matriz fuerza una decisión: **¿qué ejecutamos YA (Q1), qué planificamos (Q2-Q3), qué ignoramos?**

---

## Estructura de la matriz

Dos ejes:

### Eje Y — Impacto económico anual
Escala: USD/año en ahorro + revenue incremental.

- **Alto**: > 200K USD/año.
- **Medio**: 50K - 200K USD/año.
- **Bajo**: < 50K USD/año.

### Eje X — Effort de implementación
Escala: complejidad × tiempo × dependencias.

- **Bajo (1-2 semanas)**: herramienta existente, sin integración custom, cambio mínimo de proceso.
- **Medio (4-8 semanas)**: integración con 1-2 sistemas, cambio de proceso moderado.
- **Alto (3-6 meses)**: múltiples integraciones, cambio mayor de proceso, compliance revisado.

### Cuadrantes resultantes

```
                   Impacto
                      ↑
          ┌─────────────┬──────────────┐
     Alto │ BIG SWINGS  │ QUICK WINS ⭐ │
          │  planificar │  ejecutar ya │
          ├─────────────┼──────────────┤
     Bajo │ DEPRIORITIZE│ NICE-TO-HAVE │
          │   no tocar  │   backlog    │
          └─────────────┴──────────────┘
                    Alto       Bajo
                       ←  Effort  →
```

---

## Reglas de priorización

1. **Quick wins primero, sin excepción.** Son los que pagan el audit y construyen confianza para proyectos más grandes.
2. **Máximo 2 big swings en paralelo.** Más que eso satura capacidad interna.
3. **Nice-to-have van a backlog visible**, no se tiran. A veces pasan a quick win cuando aparece una herramienta nueva.
4. **Deprioritize se documentan con razón**. Si en 6 meses cambia algo, se revisan.

---

## Scoring detallado por oportunidad

Por cada oportunidad candidata (del output del paso 4), calcular:

### Componentes del Score

```
Score = (Impacto_normalizado × 0.5) + (Feasibility × 0.2) + (Velocidad × 0.2) + (Strategic_fit × 0.1)
```

Escala 1-5 cada componente. Score total máximo: 5.0.

#### Impacto (40%)
- 5: > 300K USD/año
- 4: 150K - 300K
- 3: 50K - 150K
- 2: 20K - 50K
- 1: < 20K

#### Feasibility (20%)
- 5: tecnología madura (LLM tasks, OCR), datos limpios.
- 4: tecnología madura, datos requieren prep.
- 3: tecnología testeada, cliente ha hecho algo similar.
- 2: tecnología de frontera, sin caso comparable.
- 1: R&D, fuera del core de JM.

#### Velocidad (20%)
- 5: < 2 semanas para ver lift.
- 4: 4-6 semanas.
- 3: 2-3 meses.
- 2: 4-6 meses.
- 1: > 6 meses.

#### Strategic fit (10%)
- 5: alineada con outcome principal del sponsor.
- 3: alineada con outcome secundario.
- 1: no alineada (descartar si esto es < 3).

---

## Template de captura por oportunidad

```
### Oportunidad #{{N}}: {{nombre}}

**Descripción:** {{1 frase clara}}
**Zona del business map:** {{Adq/Ent/Ret/Back}}
**Tarea(s) afectada(s) del task map:** T001, T007, T009...

**Problema que resuelve:**
{{2-3 frases}}

**Solución propuesta:**
{{tipo: RAG | agente | clasificación | workflow automation | ...}}
{{stack: GPT-4 + vector DB | n8n + Zapier | webhook + script}}

**Impacto esperado:**
- Horas ahorradas: {{h/sem}}
- Valor horas: USD {{anual}}
- Revenue incremental (si aplica): USD {{anual}}
- Total: USD {{anual}}

**Costo total (año 1):**
- Implementación (JM Consulting): USD {{}}
- Herramientas / licencias: USD {{}}
- API / inference: USD {{}}
- Mantenimiento: USD {{}}
- **Total:** USD {{}}

**Payback:** {{meses}}

**Effort score (1-5):** {{}}
**Semanas estimadas:** {{}}

**Dependencias:**
- {{data}}, {{sistemas}}, {{personas}}

**Riesgos:**
- {{técnico / operativo / compliance}}

**Quick win / Big swing / Nice-to-have / Deprioritize:** {{}}

**Score total:** {{X.X}} / 5.0

**Owner JM:** {{CTO / CRO / ...}}
**Owner cliente:** {{rol}}
```

---

## Ejemplo de matrix poblada — Property Management

```
| # | Oportunidad | Impacto $/año | Effort | Cuadrante | Score |
|---|---|---|---|---|---|
| 1 | Auto-respuesta IA a leads web (< 5min) | 180K | 2 (bajo) | Quick win | 4.4 |
| 2 | Clasificación y ruteo de tickets maintenance | 95K | 2 (bajo) | Quick win | 4.1 |
| 3 | Bot de QA interno (RAG sobre manuales) | 40K | 3 (medio) | Nice-to-have | 3.2 |
| 4 | Draft automático de contratos de lease | 220K | 4 (alto) | Big swing | 3.8 |
| 5 | Generación de reportes semanales al dueño | 35K | 1 (bajo) | Quick win | 4.0 |
| 6 | IA para screening de applications | 110K | 3 (medio) | Big swing | 3.6 |
| 7 | Automation de reconciliación bancaria | 15K | 2 (bajo) | Nice-to-have | 2.9 |
| 8 | Predicción de churn de inquilinos | 50K | 5 (alto) | Deprioritize | 2.4 |
| 9 | Transcripción + resumen de llamadas | 25K | 1 (bajo) | Nice-to-have | 3.1 |
| 10 | RAG manual empleados (onboarding) | 18K | 2 (bajo) | Nice-to-have | 2.8 |
```

Recomendación del audit para este cliente:
- **Trimestre 1 (Quick wins):** #1, #2, #5 → combined impact 310K USD/año.
- **Trimestre 2-3 (Big swing):** #4 → 220K adicionales.
- **Backlog:** #3, #6, #7, #9, #10.
- **Descartado:** #8 (ROI débil, data insuficiente para modelo predictivo).

---

## Visualización en el deck ejecutivo

### Slide tipo matrix

Gráfico de cuadrantes con puntos nombrados. Tamaño del punto = impacto. Color = cuadrante.

Tecnologías para renderizar:
- Matplotlib (output PNG).
- D3.js / Recharts (si es React artifact).
- Excel con chart de dispersión.

### Slide tipo tabla ranked

Lista ordenada por Score con columnas: # | Nombre | Impacto | Effort | Cuadrante | Semana start.

### Slide tipo roadmap

Gantt de 90 días con oportunidades quick win tipadas.

---

## Anti-patterns

- **Meter todo en Quick Win** porque el cliente empuja. Si hay > 5 quick wins, no hay priorización real.
- **Ignorar Big Swings** porque "asustan". Uno bien elegido paga 2 años de retainer.
- **Aceptar Impacto > 1M sin validación fuerte.** Los números grandes deben ser defendibles línea por línea.
- **Eliminar oportunidades sin documentar el por qué.** Se pierden si el cliente cambia sponsor.

---

## Output

Archivo: `/delivery/clients/{{company}}/opportunity-matrix-v1.xlsx` + PNG del gráfico.

## Referencias

- Paso previo: `/audit/task-map-template.md`
- Paso siguiente: `/audit/roi-calculator-spec.md`
- Destino en deck: `/audit/audit-deck-outline.md`
