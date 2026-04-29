# Task Map Template — Paso 3 del audit

Descomposición de cada proceso en tareas medibles, cuantificadas en tiempo y dinero.

## Filosofía

> Lo que no se cuenta, no se mejora. Y lo que no se cuenta en dinero, no se vende al board.

## Regla 1: Toda tarea en el map es cuantificada
Si no podés poner un número al lado, no entra. Si hace falta estimar, estimar con rango (p. ej. "5-8 min") pero estimar.

## Regla 2: Toda tarea tiene dueño
Si nadie la hace, no existe. Si 3 la hacen distinto, entran 3 filas.

## Regla 3: El mapa vive en XLSX
Para poder ordenar, filtrar, totalizar. El markdown de este archivo es la especificación — la data real va en una hoja Excel (ver `/audit/roi-calculator-spec.md` para el archivo completo).

---

## Columnas obligatorias

```
| # | Task | Zona | Proceso | Rol ejecutor | Frec/sem | Tiempo/vez (min) |
  | Volumen/sem | Horas/sem | Costo/hora (USD) | Costo/sem (USD) |
  | Costo/año (USD) | Sistemas | Handoff hacia | Sensibilidad datos |
  | Notas |
```

### Descripción de cada columna

- **#**: ID numérico (T001, T002...).
- **Task**: descripción concreta (verbo + objeto). Ej: "Responder lead web".
- **Zona**: Adquisición / Entrega / Retención / Back-office.
- **Proceso**: el proceso dentro de la zona (Triage, Fulfillment, Support...).
- **Rol ejecutor**: rol que la hace (no nombre propio, es reemplazable).
- **Frec/sem**: veces que se ejecuta por semana.
- **Tiempo/vez (min)**: minutos por ejecución (promedio).
- **Volumen/sem**: `Frec × executores` (si hay 3 personas haciendo lo mismo 10 veces c/u = 30).
- **Horas/sem**: `Volumen/sem × Tiempo/vez / 60`.
- **Costo/hora (USD)**: sueldo cargado / horas mensuales. Usa tabla estándar (ver abajo).
- **Costo/sem**: `Horas/sem × Costo/hora`.
- **Costo/año**: `Costo/sem × 52`.
- **Sistemas**: software tocado (CRM, Excel, email...).
- **Handoff hacia**: próximo rol / sistema que recibe el output.
- **Sensibilidad datos**: pública / interna / confidencial / regulada.
- **Notas**: observaciones cualitativas.

---

## Tabla de costo/hora estándar (USA · LATAM · USA)

Valores referenciales (cargados: sueldo + benefits + overhead ~30%).

| Rol | USA (USD/h) | LATAM (USD/h) |
|---|---|---|
| Admin / Data Entry | $22 | $10 |
| Leasing / Sales Rep | $28 | $14 |
| Operations Coordinator | $32 | $16 |
| Bookkeeper / Junior Accountant | $30 | $14 |
| Senior Accountant / CPA staff | $55 | $25 |
| Paralegal | $40 | $18 |
| Associate Lawyer | $95 | $40 |
| Senior Developer | $85 | $40 |
| Manager / Supervisor | $55 | $25 |
| Director / VP | $110 | $50 |

Si el cliente comparte su data real, usar la real. Si no, usar esta tabla y documentar el supuesto.

---

## Ejemplo de task map — Property Management (extracto)

```
| # | Task | Zona | Proceso | Rol | Frec/sem | min/vez | Vol/sem | h/sem | $/h | $/sem | $/año |
|---|---|---|---|---|---|---|---|---|---|---|---|
| T001 | Triage de leads entrantes | Adq. | Triage | Leasing | 420 | 3 | 420 | 21 | 28 | 588 | 30.6K |
| T002 | Primera respuesta email/SMS | Adq. | Outreach | Leasing | 420 | 6 | 420 | 42 | 28 | 1176 | 61.2K |
| T003 | Scheduling de tour | Adq. | Tour | Leasing | 180 | 8 | 180 | 24 | 28 | 672 | 34.9K |
| T004 | Follow-up lead frío | Adq. | Nurture | Leasing | 140 | 5 | 140 | 11.7 | 28 | 327 | 17.0K |
| T005 | Ticket de maintenance | Ent. | Tickets | Ops | 80 | 12 | 80 | 16 | 32 | 512 | 26.6K |
| T006 | Dispatcheo a vendor | Ent. | Tickets | Ops | 80 | 8 | 80 | 10.7 | 32 | 341 | 17.7K |
| T007 | Follow-up al residente | Ent. | Tickets | Ops | 60 | 5 | 60 | 5 | 32 | 160 | 8.3K |
| T008 | Reconciliación bancaria | Back | Finanzas | Bookk | 1 | 180 | 1 | 3 | 30 | 90 | 4.7K |
| T009 | Armado de reporte semanal al dueño | Back | Reporting | Ops Coord | 20 | 45 | 20 | 15 | 32 | 480 | 25.0K |
| T010 | Actualización de rent roll | Back | Data | Admin | 5 | 30 | 5 | 2.5 | 22 | 55 | 2.9K |
```

Total anual capturado en este extracto: **~229K USD/año** de horas humanas sólo en estas 10 tareas.

---

## Proceso de captura de tareas

### Fuentes
1. **Entrevistas Yesterday Morning** → origen principal.
2. **Observación directa / shadowing** → complemento.
3. **Reportes de sistemas** (tickets totales, leads totales) → validación de volumen.
4. **HR** → nómina por rol para estimar costo/hora.

### Flujo de trabajo
1. Durante entrevistas, anotar tareas en "draft task list" (post-it / notas).
2. Cada noche pasar al XLSX real.
3. Cuantificar frec/tiempo con la persona (si quedó pendiente, preguntar por Slack).
4. Marcar con `?` las estimaciones débiles para validar después.
5. Al final de la semana, revisar con sponsor los totales.

---

## Reglas de calidad del task map

### Criterios para incluir
- Consume ≥ **2 h/sem** a alguien, O
- Tiene volumen ≥ **20 ejecuciones/sem** (aunque sean cortas), O
- Tiene riesgo de error con impacto > 1K USD por evento, O
- Es handoff crítico entre zonas.

### Criterios para NOT incluir
- Tareas que suceden < 1 vez/mes y toman < 30 min.
- Cosas que solo hace una persona senior y no son candidatas a automation.
- "Pensar en estrategia" → no es tarea, es trabajo.

---

## Subtotales y analíticas

Al cierre del task map, calcular:

```
1. Total horas/sem capturadas:            X
2. Total USD/año capturadas:              Y
3. % del headcount total capturado:       X / horas_totales_empresa
4. Top 10 tareas por costo/año
5. Top 10 tareas por horas/sem
6. Total por zona (Adq / Ent / Ret / Back)
```

Estos subtotales alimentan el opportunity matrix.

---

## Checkpoint

El task map está listo para pasar al paso 4 (AI Feasibility) cuando:
- [ ] Mínimo 40 tareas mapeadas (empresa mediana; 20 para pequeña).
- [ ] 80% cuantificadas con fuente (no solo estimadas).
- [ ] Totales validados por sponsor.
- [ ] Top 10 por costo tiene owner explícito.

---

## Output final

Archivo XLSX: `/delivery/clients/{{company}}/task-map-v1.xlsx`
- Hoja 1: `tasks` (datos crudos).
- Hoja 2: `pivot_by_zone` (totales por zona).
- Hoja 3: `top_by_cost` (ranked).
- Hoja 4: `systems_impact` (qué sistemas tocan más horas).
- Hoja 5: `assumptions` (tabla de supuestos usados).

---

## Referencias

- Paso previo: `/audit/business-map-template.md`
- Paso siguiente: Filtro de AI Feasibility → `/audit/roi-first-framework.md#paso-4`
- Output destino: `/audit/opportunity-matrix.md`
- Cálculo final: `/audit/roi-calculator-spec.md`
