# Implementation Scope — Definición de alcance

Cómo se especifica el scope de cada workstream (cada oportunidad se vuelve un workstream).

## Filosofía

> Scope claro = ejecución rápida. Scope difuso = death by 1000 cuts.

Todo workstream en `/delivery/clients/{{company}}/workstreams/{{nombre}}/` arranca con `scope.md`. Sin scope firmado, no hay implementación.

---

## Plantilla de scope (markdown)

```markdown
# Workstream: {{nombre_corto}}
Proyecto: {{Company}} · Audit ID: {{id}} · Versión scope: 1.0 · Fecha: {{date}}

## Owner
- Owner JM: {{rol + nombre}}
- Owner Cliente: {{rol + nombre}}
- Sponsor Cliente: {{quién firma el gasto}}

## Objetivo

{{1 párrafo describiendo qué se resuelve y por qué}}

## Outcome asociado

Esta implementación mueve la métrica **{{métrica}}** de baseline **{{X}}** hacia target **{{Y}}** en **{{N}}** semanas.

## In Scope

- {{acción concreta 1}}
- {{acción concreta 2}}
- {{acción concreta 3}}
...

## Out of Scope (explícito)

- {{lo que NO se hace, aunque alguien lo pida}}
- {{NO se toca el sistema X}}
- {{NO se incluyen casos de uso Y}}

## Arquitectura propuesta

### Componentes
- {{LLM provider}}: {{modelo}}, {{modo}}.
- {{Vector DB}}: {{cuál}}, {{tamaño}}.
- {{Automation}}: {{n8n / Zapier / custom}}.
- {{Integraciones}}: {{sistema cliente A, B, C}}.
- {{UI}}: {{Slack bot / web / ninguno}}.

### Data flow (mermaid)
\`\`\`mermaid
graph LR
    Input --> Pre[Preprocessing]
    Pre --> Model[LLM / clasificador]
    Model --> Post[Postprocessing]
    Post --> Output
    Output --> Sink[Sistema destino]
\`\`\`

### Supuestos críticos
- {{supuesto 1}}: si no se cumple, impacto X.
- {{supuesto 2}}: si no se cumple, impacto Y.

## Criterios de aceptación

Marcadores binarios de "terminado":

- [ ] {{criterio 1}} — medible y testeable.
- [ ] {{criterio 2}}.
- [ ] {{criterio 3}}.
- [ ] Métrica {{métrica}} llega a {{target}} en pre-prod.
- [ ] Equipo cliente capacitado (2 sesiones).
- [ ] Runbook de operación escrito.
- [ ] Plan de rollback escrito.

## Entregables técnicos

- Código en repo {{url}}.
- Workflows n8n en {{env}}.
- Documentación en {{Paperclip/Notion/docs}}.
- Credenciales transferidas a {{vault cliente}}.
- Scripts de migración / backfill.
- Dashboard de monitoreo.

## Entregables de conocimiento

- Manual de usuario (PDF + video 10 min).
- Manual de operador (PDF + video 15 min).
- FAQ inicial.
- Escalation path (quién llamar si X falla).

## Cronograma

| Semana | Milestone | Entregable |
|---|---|---|
| 1 | Kickoff + accesos | Accesos activos, spec v1 firmada |
| 2 | Prototipo funcional | Demo interna |
| 3 | Piloto en sandbox | Testing con datos reales |
| 4 | Rollout a 20% usuarios | Monitoreo activo |
| 5 | Rollout a 100% | Métricas a baseline |
| 6 | Revisión + ajustes | Signoff del sponsor |

## Dependencias del cliente

- [ ] Accesos a {{sistema A}} con permisos {{nivel}}.
- [ ] Datos históricos de {{X}} meses para training/validación.
- [ ] 1 empleado operador disponible 4 h/semana para feedback.
- [ ] Sponsor disponible 30 min/semana para decisiones.

## Riesgos top 3

| # | Riesgo | Probab. | Impacto | Mitigación |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

## Presupuesto

- Implementación JM: USD {{}}.
- Tools (anual): USD {{}}.
- API / inference (anual estimado): USD {{}}.
- Mantenimiento (anual): USD {{}}.
- **Total año 1**: USD {{}}.

Facturación: {{hitos de pago}}.

## Out-of-contract clauses

- Cambios de scope requieren Change Order firmado.
- Re-planificación por delays del cliente: sin costo JM.
- Re-planificación por delays JM: absorbido por JM.
- Acceso fallido a sistemas > 14 días: project pause + replan.

## Firma

Sponsor Cliente: __________________ Fecha: __________
JM Consulting:   Javier Mendoza     Fecha: __________
```

---

## Reglas de escritura del scope

### In Scope

- Máximo 10 bullets. Si hay más, es porque el workstream es demasiado grande y hay que dividir.
- Cada bullet empieza con verbo: "Implementar...", "Integrar...", "Configurar...".
- Sin adverbios de aspiración ("idealmente", "si es posible").

### Out of Scope

- Escribir al menos 5 items.
- Sirve tanto para proteger al equipo como para dar permiso al cliente de saber qué NO esperar.
- Items típicos: "No se incluye migración de data histórica > 2 años", "No se desarrolla mobile app", "No se tocan reportes existentes".

### Criterios de aceptación

- Deben ser **testeables por el cliente, sin ayuda JM**.
- Si un criterio es "el cliente está contento", no es criterio — es deseo. Reemplazar con métrica.

### Supuestos

- Al menos 3. Si no hay supuestos, no pensaste lo suficiente.
- Escribir "si NO se cumple, pasa X" es la mejor forma de descubrir riesgos ocultos.

---

## Change Orders

Cuando el cliente pide algo fuera del scope vigente:

1. PM JM emite Change Order (CO) en formato corto.
2. CO tiene: descripción, impacto en cronograma, impacto en costo.
3. Sponsor firma (email explícito válido).
4. Se actualiza `scope.md` a versión 1.1, 1.2...
5. Historial visible en el archivo.

### Template de Change Order

```
# Change Order #{{N}} — {{workstream}}
Fecha: {{date}}

**Solicitado por:** {{rol + nombre}} el {{fecha}} via {{canal}}.

**Descripción:**
{{qué se pide}}

**Justificación del cliente:**
{{por qué lo piden}}

**Análisis JM:**
- Impacto en scope actual: {{qué cambia}}.
- Impacto en cronograma: {{+X semanas}}.
- Impacto en costo: USD {{+Y}}.
- Riesgos nuevos: {{listado}}.

**Decisión:**
[ ] Aprobado — integrar al scope.
[ ] Rechazado — mantener scope original.
[ ] Deferred — registrar en backlog fase 2.

**Firma:**
Sponsor Cliente: __________ Fecha: __________
```

---

## Archivo maestro de scope del proyecto

Al nivel proyecto (no workstream), mantener `implementation-master-scope.md`:

```
# {{Company}} — Master Scope
Versión: 1.0 · Fecha: {{date}}

## Workstreams activos
| # | Nombre | Owner JM | Start | End | Scope link |
|---|---|---|---|---|---|
| 1 | Lead response AI | CTO | 2026-02-01 | 2026-03-15 | workstreams/quickwin-1/scope.md |
| 2 | Ticket classification | CTO | 2026-02-15 | 2026-04-01 | workstreams/quickwin-2/scope.md |

## Workstreams en backlog
| # | Nombre | Prioridad | Trigger |
|---|---|---|---|
| | | | |

## Change Order Log
| CO# | Workstream | Descripción | Estado | Fecha |
|---|---|---|---|---|

## Métricas consolidadas
{{Resumen de outcome metrics}}

## Riesgos a nivel proyecto (no workstream)
```

---

## Ver también

- `/delivery/handoff-template.md` — cómo se llega a este punto
- `/delivery/quick-wins-sprint.md` — cómo arranca el primer workstream
- `/delivery/qa-checklist.md` — validación de criterios de aceptación
- `/delivery/rollout-plan.md` — cómo se sale de pre-prod a prod
