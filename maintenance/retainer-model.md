# Retainer Model — Modelo de mantenimiento y AI Operations

Cómo se estructura el servicio recurrente post-implementación. **Esto es el corazón del revenue predecible de JM Consulting.**

## Filosofía

> El audit paga el gas. El retainer paga el motor.

El cliente no entra a JM para comprar código que funcionará solo. Entra para comprar **infraestructura operativa viva**: modelos que mejoran, workflows que se mantienen al día, y un equipo que entiende su negocio.

## Regla comercial

Todo cliente que implementa > 1 quick win pasa automáticamente a retainer, salvo objeción explícita.

---

## Niveles de retainer

### Tier 1 — Monitor (2K USD/mes)
Para implementaciones estables de bajo riesgo.

**Incluye:**
- Monitoring 24/7 con alertas.
- Hasta 4 horas/mes de intervención técnica.
- 1 revisión mensual (60 min).
- Acceso a roadmap trimestral de mejoras.
- SLA: respuesta en 24 h hábiles a incidentes no críticos, 2 h a críticos.

**Exclusiones:**
- Desarrollo de nuevas features.
- Re-entrenamiento de modelos.
- Integraciones nuevas.

### Tier 2 — Optimize (5K USD/mes)
Para clientes con 2-3 workstreams activos.

**Incluye:**
- Todo lo de Tier 1.
- Hasta 12 horas/mes de intervención técnica.
- 2 revisiones mensuales (60 min).
- 1 optimization cycle por trimestre (ver `/maintenance/optimization-cycle.md`).
- Updates de prompts / modelos incluidos.
- SLA: 12 h hábiles no críticos, 1 h críticos.

**Incluye hasta 1 "pequeña mejora" al mes** (1-2 días de trabajo).

### Tier 3 — Evolve (10K USD/mes)
Para clientes estratégicos con múltiples implementaciones y crecimiento activo.

**Incluye:**
- Todo lo de Tier 2.
- Hasta 30 horas/mes de intervención.
- Revisión quincenal (60 min).
- Strategic advisory trimestral con CEO/COO (120 min).
- Optimization cycle mensual.
- Re-entrenamientos incluidos.
- Monitoring de innovation: JM reporta qué nuevas capacidades IA podrían aplicar al cliente.
- SLA: 6 h hábiles no críticos, 30 min críticos.

**Incluye hasta 1 workstream mediano al trimestre.**

### Tier 4 — Fractional AI Team (20-50K USD/mes)
Para clientes grandes (>200 empleados) que no quieren contratar head of AI interno todavía.

- Equipo dedicado JM (1-3 personas).
- Presencia semanal onsite si aplica.
- Ownership completo de la capa IA del cliente.
- SLA: respuesta inmediata en horario laboral, 2 h fuera.

---

## Qué incluye cada retainer (detalle)

### 1. Monitoring
- Dashboard con KPIs técnicos y de negocio.
- Alertas configuradas.
- Reporte semanal automatizado (ver `/maintenance/monthly-review-template.md`).

### 2. Mantenimiento correctivo
- Fix de bugs.
- Actualización de prompts cuando el LLM provider cambia versiones.
- Migración de modelos deprecated.
- Reparación de integraciones caídas.

### 3. Mantenimiento preventivo
- Revisión mensual de accuracy.
- Refactoring cuando hay deuda técnica visible.
- Actualización de dependencias.

### 4. Mejora continua
- Ajustes a prompts basados en feedback operador.
- A/B tests de variaciones.
- Re-calibración de thresholds.

### 5. Advisory
- Cliente consulta sobre cualquier decisión IA sin costo extra.
- JM proactivamente sugiere optimizaciones.
- Acceso a "qué está pasando en el mercado" trimestralmente.

### 6. Capacitación continua
- Nuevos empleados del cliente reciben training (hasta 2 sesiones/mes).
- FAQ mantenido al día.
- Documentación evoluciona con cambios.

---

## Pricing y facturación

### Estructura
- Pago mensual, factura día 1 del mes.
- Contrato mínimo: 6 meses.
- Renovación automática salvo aviso con 30 días.
- Descuento de 10% por pago anual adelantado.
- Descuento adicional de 5% si el cliente permite usar el caso (anonimizado) en marketing.

### Escalation
- Si el cliente consume 2 meses seguidos > 120% de las horas incluidas, JM sugiere tier upgrade.
- Si consume < 40% durante 3 meses, JM sugiere downgrade (ofrecer antes de que el cliente pida cancelar).

### Horas adicionales
- Si el cliente necesita trabajo que excede el tier:
  - Se emite Change Order.
  - Se facturan al rate estándar (USD 150/h senior, USD 80/h junior).
  - No se usan horas del retainer para esto — el retainer es para mantenimiento/advisory, no desarrollo nuevo.

---

## Matriz de servicios incluidos por tier

| Servicio | Tier 1 | Tier 2 | Tier 3 | Tier 4 |
|---|---|---|---|---|
| Monitoring 24/7 | ✅ | ✅ | ✅ | ✅ |
| Horas intervención/mes | 4 | 12 | 30 | 80+ |
| Revisiones mes | 1 | 2 | 2 + quincenal | Semanal |
| Strategic advisory | — | — | Trimestral | Continuo |
| Optimization cycle | — | Trimestral | Mensual | Continuo |
| Pequeñas mejoras | — | 1/mes | 3/mes | Continuo |
| Workstreams medianos | — | — | 1/trimestre | 1/mes |
| Re-training modelos | — | — | ✅ | ✅ |
| Innovation monitoring | — | — | ✅ | ✅ |
| SLA crítico | 2 h | 1 h | 30 min | Inmediato |
| SLA no crítico | 24 h | 12 h | 6 h | 2 h |

---

## Dimensionamiento inicial del cliente

Regla de entrada:
- 1-2 workstreams en prod → Tier 1.
- 3-4 workstreams → Tier 2.
- 5+ workstreams o workstream estratégico crítico → Tier 3.
- Enterprise (>200 empleados, multi-site) → Tier 3 o 4.

---

## Churn y retención

### Signals que un retainer está en riesgo
- Consumo < 30% de horas 2 meses seguidos.
- Sponsor cambia en el cliente (sin handoff).
- Cliente pide descuento o re-negociación.
- Baja asistencia a monthly review.
- Silencio prolongado (> 3 semanas sin interacción).

### Plan de retención proactiva
- Cuando aparece un signal, agenda llamada con sponsor en 7 días.
- Llevar 1 insight de valor no solicitado ("encontré esto mirando sus logs").
- Revisar outcomes actuales vs originales — si ya se cumplieron, proponer nuevos.

### Off-boarding limpio
Si el cliente decide cancelar:
- 30 días de transition.
- Transferencia completa de código, docs, credenciales.
- Sesión de knowledge transfer al equipo técnico del cliente.
- Puerta abierta para re-enganche.
- Pedir referral.

---

## Upsell paths

De Tier 1 a Tier 2: cuando implementa el segundo workstream.

De Tier 2 a Tier 3: cuando hay necesidad de advisory estratégico o segundo año activo.

De Tier 3 a Tier 4: cuando el cliente empieza a pensar en contratar head of AI interno.

De retainer a proyecto grande: cuando el business map muestra nueva fuga detectada.

---

## KPIs del modelo de retainer (interno JM)

- **GRR** (Gross Revenue Retention): > 90% anual.
- **NRR** (Net Revenue Retention): > 110% anual (upsell > churn).
- **NPS retainer clients**: > 40.
- **Avg tenure**: > 18 meses.
- **% clientes en Tier ≥ 2**: > 60%.

---

## Ver también

- `/maintenance/monthly-review-template.md` — formato de revisión mensual
- `/maintenance/incident-response.md` — SLAs y escalation
- `/maintenance/optimization-cycle.md` — qué se hace trimestralmente
- `/company/service-ladder.md` — contexto general del modelo de servicios
