# ROI Calculator — Especificación del XLSX

Especificación del archivo Excel que entregamos al cliente junto con el deck. Es el activo que **convierte abstractos en números defendibles ante el board**.

## Objetivo

Un archivo interactivo donde el cliente puede ajustar supuestos (costo/hora, volumen, % ahorro esperado) y ver cómo cambia el ROI. Rompe la objeción "¿cómo calculaste eso?".

---

## Estructura del archivo

Nombre: `ROI_Calculator_{{company}}_v1.xlsx`

### Hoja 1: `README`

Instrucciones al cliente:

```
ROI Calculator — {{company}}
Versión 1.0 · Fecha {{date}}

Cómo usar:
1. Edita celdas amarillas. Las grises son fórmulas (no tocar).
2. La pestaña "Supuestos" es el corazón: cambia valores allí.
3. La pestaña "Opportunities" muestra ROI por oportunidad.
4. La pestaña "Dashboard" muestra el total.
5. Si un supuesto no aplica a tu caso, ajústalo.

Garantía: si los números base (horas, costos) están correctos,
el ROI es conservador. Hemos ajustado 20% de margen hacia abajo
en ahorros proyectados.
```

### Hoja 2: `Supuestos`

Celdas amarillas (editables) con valores clave.

```
| Categoría | Variable | Valor | Unidad | Notas |
|---|---|---|---|---|
| Global | Días laborales/año | 260 | días | 52 sem × 5 |
| Global | Semanas activas/año | 50 | semanas | -2 vacaciones |
| Global | % overhead sueldo | 30% | % | HR + oficina + tax |
| Costos | Admin USD/h | 22 | USD | cargado |
| Costos | Leasing USD/h | 28 | USD | cargado |
| Costos | Ops Coord USD/h | 32 | USD | cargado |
| Costos | Bookkeeper USD/h | 30 | USD | cargado |
| Costos | CPA Senior USD/h | 55 | USD | cargado |
| IA | GPT-4 tokens in (USD/1M) | 5 | USD | OpenAI pricing |
| IA | GPT-4 tokens out (USD/1M) | 15 | USD | OpenAI pricing |
| IA | Vector DB (USD/mes) | 70 | USD | Pinecone/Weaviate |
| Implementación | JM rate senior (USD/h) | 150 | USD | |
| Implementación | JM rate junior (USD/h) | 80 | USD | |
| Mantenimiento | Retainer estándar (USD/mes) | 3500 | USD | |
```

### Hoja 3: `Task_Map`

Importado del task map (paso 3).

Columnas:
```
# | Task | Zona | Rol | Frec/sem | min/vez | Vol/sem | h/sem | $/h | $/sem | $/año
```

Fórmulas:
- `h/sem = Vol/sem * min/vez / 60`
- `$/sem = h/sem * $/h`
- `$/año = $/sem * 50`

### Hoja 4: `Opportunities`

Por cada oportunidad identificada, un bloque.

```
Oportunidad #1: Auto-respuesta IA a leads

INPUTS (editables - amarillo):
- Tasks afectadas:                T001, T002
- % tiempo ahorrado:               85%
- Revenue incremental anual:       120,000 USD
- Costo implementación JM:         18,000 USD
- Costo tools anual:               2,400 USD (API + Instantly + etc.)
- Costo mantenimiento anual:       6,000 USD
- Costo change mgmt anual:         3,000 USD

CÁLCULOS (grises):
- Horas ahorradas/sem:             = sum(h/sem de tasks) * % ahorro
- Costo horas ahorradas anual:     = h/sem_ahorradas * $/h * 50
- Beneficio total anual:           = ahorro + revenue_incremental
- Costo total año 1:               = sum(implementación + tools + mgmt + change)
- ROI año 1 (%):                   = (Beneficio - Costo) / Costo * 100
- Payback (meses):                 = Costo_año_1 / (Beneficio / 12)
- VAN 3 años (@10%):              = VAN(10%, [flujos])
```

Un bloque por oportunidad (mínimo top 10).

### Hoja 5: `Dashboard`

Consolidación.

```
CONSOLIDADO — {{company}}

Oportunidades quick win (Q1):
| # | Nombre | Beneficio año 1 | Costo año 1 | ROI | Payback |
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

Subtotal Quick wins:            {{sum}}

Oportunidades big swing (Q2-Q3):
| # | Nombre | Beneficio año 1 | Costo año 1 | ROI | Payback |
| 4 | | | | | |

TOTAL AUDIT RECOMENDADO:
- Inversión año 1:               {{}}
- Beneficio año 1:               {{}}
- Beneficio año 2 (lift):        {{}}
- Beneficio año 3:               {{}}
- VAN 3 años @ 10%:              {{}}
- TIR:                           {{}}
- Payback medio:                 {{meses}}

Top 3 sensibilidades (qué cambia si cambiamos supuestos):
- Si costo/hora sube 20%: ROI pasa de X% a Y%.
- Si volumen baja 30%: ROI pasa de X% a Y%.
- Si implementación se atrasa 2 meses: ROI pasa de X% a Y%.
```

### Hoja 6: `Sensitivity`

Tabla de sensibilidad 2D (volumen vs costo/hora, por ejemplo).

Permite ver el rango de ROI en escenarios pesimistas / optimistas.

### Hoja 7: `Benchmarks`

Referencias de ROI en casos comparables (anonimizados):

```
| Industria | Empleados | Oportunidad | ROI año 1 | Payback |
|---|---|---|---|---|
| Property Mgmt | 60 | Lead response | 310% | 3 meses |
| Accounting | 30 | Doc automation | 420% | 2 meses |
| Legal | 20 | Contract draft | 280% | 4 meses |
```

### Hoja 8: `Change_Log`

Versión, fecha, cambios. Para audit trail.

---

## Fórmulas clave (para replicar)

### Costo de horas humanas
```
Costo_anual = Volumen_semanal × Tiempo_por_vez_min / 60 × Costo_hora × Semanas_activas_año
```

### ROI año 1
```
ROI = (Beneficio_total - Costo_total) / Costo_total × 100
```

### Payback
```
Payback_meses = Costo_año_1 / (Beneficio_total_año_1 / 12)
```

### VAN 3 años
```
VAN = sum_t=0..3 [Flujo_t / (1 + tasa)^t]
donde Flujo_0 = -Inversión, Flujo_1..3 = Beneficio - Mantenimiento
tasa = 10% (default, editable)
```

### TIR
Función `=TIR(flujos)` de Excel directamente.

---

## Reglas de implementación

### Formato visual
- Celdas amarillas = editables.
- Celdas grises = fórmulas (proteger con password).
- Headers en azul oscuro, blanco sobre azul.
- Números con separador de miles.
- Currency con símbolo USD.
- Porcentajes con 1 decimal.

### Protección
- Todas las hojas protegidas con password (cliente solo edita amarillas).
- Password = primera letra de cada hoja + fecha del audit.

### Métodos de cálculo a usar
- No usar macros (clientes corporativos las bloquean).
- Usar funciones estándar: SUM, SUMIF, IF, VLOOKUP, NPV, IRR.
- Data validation donde corresponda (dropdowns para selección de rol, zona).

---

## Conservadurismo explícito

Regla de oro: **si el número del cliente sorprende para bien, reducilo 20% antes de presentarlo.**

Preferimos sub-prometer y sobre-entregar. Si el cálculo crudo da 450K USD/año, presentar 350K.

Documentar el haircut en la hoja Supuestos explícitamente:
```
Margen de conservadurismo aplicado: 20% (estándar JM)
```

---

## Entrega al cliente

1. XLSX firmado digitalmente (si posible).
2. Versión PDF congelada como snapshot.
3. Walk-through de 30 min explicando cómo tocarlo.
4. Slack canal abierto para consultas de supuestos en las 2 semanas siguientes.

---

## Generación automática

Para escalar, crear un script Python que:
1. Lea el task map CSV.
2. Lea oportunidades y supuestos JSON.
3. Genere XLSX con openpyxl (o xlsxwriter) usando plantilla maestra.
4. Aplique fórmulas.
5. Genere PDF con libreoffice --convert-to.

Script objetivo: `/scripts/generate_roi_calculator.py` (backlog de automation interna).

---

## Referencias

- Paso previo: `/audit/opportunity-matrix.md`
- Paso siguiente: `/audit/audit-deck-outline.md`
- Template físico: `/assets/roi_calculator/ROI_Calculator_MASTER.xlsx`
