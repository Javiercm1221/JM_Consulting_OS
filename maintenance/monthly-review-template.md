# Monthly Review Template — Revisión mensual con cliente

Formato estándar de la reunión mensual con cada cliente en retainer. Este es el momento donde JM demuestra valor y detecta nuevas oportunidades.

## Propósito

1. Revisar métricas del mes.
2. Escuchar feedback del cliente.
3. Mostrar mejoras hechas.
4. Proponer próximas acciones.
5. Mantener relación.

## Duración

60 minutos estándar (Tier 2+), 45 minutos Tier 1.

## Participantes

- Del lado JM: Owner del cliente (account lead) + técnico principal (opcional).
- Del lado cliente: Sponsor + 1-2 usuarios / operadores principales.

---

## Agenda tipo (60 min)

### 1. Apertura y contexto (5 min)
- Cómo estuvo el mes desde el punto de vista del cliente.
- ¿Algo cambió en el negocio?
- ¿Algún "temón" pendiente? (mejor sacarlo al principio)

### 2. Métricas del mes (15 min)
Presentar dashboard con:
- Outcome principal (lift vs baseline).
- Métricas técnicas (uptime, accuracy, latency).
- Métricas de uso (volumen, adopción).
- Costos (API + infra + horas).

Formato sugerido: 1 página de dashboard + comentarios en vivo.

### 3. Highlights y wins (5 min)
- Qué funcionó especialmente bien.
- Casos específicos (quotes de operadores si hay).
- Cómo esto se traduce a USD ahorrados / ganados este mes.

### 4. Issues y resoluciones (10 min)
- Incidentes del mes (si hubo): qué pasó, cómo se resolvió, qué cambió.
- Tickets abiertos: status.
- Feedback crítico recibido.

### 5. Mejoras hechas (10 min)
- Qué se tocó sin que el cliente pidiera (proactivo).
- Qué se liberó en el backlog por pedido.
- Cómo se mide la mejora.

### 6. Próximo mes — plan (10 min)
- 3 focos del mes siguiente.
- Owner de cada uno.
- Deliverables esperados.
- Riesgos identificados.

### 7. Strategic pulse (5 min)
- ¿Qué oportunidades nuevas aparecieron en el business map?
- ¿Algo que cambió en el entorno del cliente merece revisión del roadmap?
- ¿Algún pedido fuera del scope actual que evaluar?

### 8. Cierre (5 min minutes)
- Action items con dueño y fecha.
- Confirmación de próxima sesión.
- Feedback libre.

---

## Plantilla de notas (markdown)

Archivo: `/delivery/clients/{{company}}/status/monthly-review-{{YYYY-MM}}.md`

```markdown
# Monthly Review — {{Company}} — {{YYYY-MM}}
Fecha: {{date}} · Duración: {{min}} · Grabación: {{link}}

## Asistentes
- JM: {{nombre}} ({{rol}})
- Cliente: {{nombre}} ({{rol}}), {{nombre}} ({{rol}})

## Contexto del mes
{{qué cambió en el cliente}}

## Métricas

### Outcome primario: {{nombre métrica}}
- Baseline: {{valor}}
- Target: {{valor}}
- Actual: {{valor}} ({{▲/▼}} vs mes anterior {{%}})

### Otros KPIs
| Métrica | Target | Actual | Tendencia |
|---|---|---|---|

### Uso / Adopción
- % equipo usando sistema: {{%}}
- Volumen procesado: {{N}}
- Tasa de re-trabajo humano: {{%}}

### Costos
- API (USD): {{}}
- Infra (USD): {{}}
- Horas JM consumidas: {{N}} / {{limite tier}}

## Wins del mes
1.
2.
3.

## Issues
| # | Issue | Severidad | Resolución | Estado |
|---|---|---|---|---|

## Mejoras aplicadas este mes
- {{tipo}} ({{ticket}}): {{descripción}} → {{impacto}}.

## Plan próximo mes
1. {{foco 1}} — owner: {{nombre}} — deadline: {{fecha}}.
2. {{foco 2}} — idem.
3. {{foco 3}} — idem.

## Oportunidades nuevas detectadas
- {{en qué parte del business map apareció}}
- {{tamaño estimado del upside}}

## Action items
- [ ] {{acción}} — {{owner}} — {{due date}}.
- [ ] ...

## Quotes / feedback del cliente
> "..."

## Próxima reunión
{{fecha + hora}}
```

---

## Dashboard — componentes obligatorios

### Bloque 1: Outcome
Gráfico de línea de la métrica primaria (últimos 90 días) con línea de baseline y target marcadas.

### Bloque 2: Uso
Barras: volumen procesado por día / semana del mes.

### Bloque 3: Calidad
- Accuracy del mes (línea con accuracy semanal).
- Tasa de re-trabajo humano.
- NPS del operador (si se midió).

### Bloque 4: Reliability
- Uptime.
- Latency p95.
- Error rate.
- Incidentes (# sev1, # sev2).

### Bloque 5: Costo
- API cost / día.
- Proyección mensual vs presupuesto.
- Costo por transacción procesada.

---

## Reglas del consultor durante la sesión

### Hacer
- **Ir con dashboard pre-compartido** 24 h antes.
- **Traer 1 insight no pedido** ("vi esto en los logs la semana pasada").
- **Preguntar por 1 área fuera del scope actual** (para detectar oportunidades nuevas).
- **Anotar quotes literales** del sponsor para usar internamente en caso de que venga a cuenta (upsell, renovación, caso de estudio).
- **Cerrar con action items claros**.

### No hacer
- **No llegar sin dashboard**.
- **No justificar números malos** — explicarlos y actuar.
- **No vender al medio de la sesión.** Strategic pulse al final.
- **No prometer en vivo lo que no estés seguro**. Mejor "te confirmo en 48 h".

---

## Señales para escalar la conversación

Si aparece alguno de estos durante la sesión, seguir especialmente de cerca:

1. Sponsor menciona nuevo proyecto/iniciativa → detectar oportunidad.
2. Sponsor menciona cambio organizacional → posible impacto al retainer.
3. Sponsor comparte frustración con otro proveedor → posible displacement.
4. Sponsor menciona benchmark con competidor → oportunidad de defender + upsell.

---

## Follow-up post-sesión

En < 24 h, enviar email con:
- Resumen escrito de los action items (dueño + fecha).
- Links a cualquier recurso prometido.
- Confirmación de próxima fecha.
- Quote de cierre positivo.

---

## Frecuencia de revisiones especiales

### Weekly stand-up (15 min)
- Solo durante Tier 3 / Tier 4.
- Focus: tactical.
- Formato: Slack async + 15 min call si hay tema.

### Monthly review (60 min)
- Tier 2 y Tier 3.
- Focus: métricas + near-term plan.
- Formato: videocall con dashboard.

### Quarterly business review (120 min)
- Tier 3 / Tier 4.
- Focus: strategic + roadmap anual.
- Con CEO / COO del cliente.
- Incluye: recap del trimestre, oportunidades nuevas, propuesta Q+1.

### Annual review (half-day)
- Tier 4 o clientes > 1 año.
- Focus: visión anual, renovación.
- Incluye: presentación de outcomes year-over-year, caso de estudio interno del cliente, roadmap anual nuevo.

---

## Ver también

- `/maintenance/retainer-model.md` — estructura general del retainer
- `/maintenance/optimization-cycle.md` — trabajo trimestral
- `/maintenance/incident-response.md` — cuando hay un incidente entre revisiones
