# Incident Response — Respuesta a incidentes

Protocolo para incidentes en producción. **Si algo falla en un cliente, así se gestiona.**

## Filosofía

> Un incidente no es fracaso. Un incidente mal gestionado, sí.

La velocidad + la transparencia del consultor durante un incidente son los momentos donde más se gana o se pierde confianza del cliente.

---

## Definiciones de severidad

### Sev 1 — Crítico
Algo está caído o causando daño activo.
- Sistema no responde.
- Data loss o corrupción.
- Decisiones incorrectas con impacto financiero > 1K USD/hora.
- Violación de compliance detectada.
- Vulnerabilidad de seguridad activa.

**SLA respuesta:** 30 min (Tier 3), 1 h (Tier 2), 2 h (Tier 1).
**SLA resolución:** < 4 h o mitigación activa.

### Sev 2 — Grave
Funcionalidad degradada pero no caída.
- Accuracy cae < target.
- Latency supera 3× baseline.
- Integración con 1 sistema cliente cae.
- Feature no-crítica no funciona.

**SLA respuesta:** 2 h (Tier 3), 6 h (Tier 2), 12 h (Tier 1).
**SLA resolución:** < 24 h hábiles.

### Sev 3 — Menor
Bug sin impacto operativo significativo.
- Error cosmético.
- Edge case que afecta < 1% del volumen.
- Request de información.

**SLA respuesta:** 1 día hábil.
**SLA resolución:** según backlog y prioridad.

### Sev 4 — Info / Pregunta
No es un incidente; es una consulta.
- "¿Cómo hago X?"
- "¿Podemos cambiar Y?"

**SLA respuesta:** 1-2 días hábiles.

---

## Protocolo de respuesta — Sev 1

### Paso 1: Detección (minuto 0)
Fuentes típicas:
- Alerta automática (dashboard, PagerDuty).
- Cliente reporta (Slack, email, teléfono).
- Miembro JM detecta en review rutinario.

### Paso 2: Acknowledgment (minuto 0-5)
El primer JM que recibe el aviso:
1. Confirma recepción al cliente ("Recibido. Estoy en eso ahora.").
2. Inicia "war room" (canal Slack o huddle).
3. Avisa al account lead y al técnico principal.

### Paso 3: Triage (minuto 5-30)
- ¿Qué está pasando exactamente?
- ¿Desde cuándo?
- ¿Qué está afectado y qué no?
- ¿Hay daño activo? ¿Podemos pausarlo?

**Decisión inmediata:** ¿rollback o fix forward?

### Paso 4: Mitigación (minuto 0-60 idealmente)
Prioridad 1: **detener el daño**. Aunque sea con solución temporal.

Opciones comunes:
- Rollback al último estado estable.
- Activar feature flag de fallback.
- Desactivar el workflow afectado, volver a proceso manual.
- Escalar capacidad si es load issue.

### Paso 5: Comunicación al cliente (cada 30-60 min)
Formato corto, claro:
```
[UPDATE {{HH:MM}}]
Status: {{mitigación activa / investigando / resuelto}}.
Impacto actual: {{nada / X% volumen afectado / etc.}}.
Causa raíz preliminar: {{hipótesis}}.
Próximo paso: {{acción + ETA}}.
```

Aunque no haya progreso, mandar "sin novedad, seguimos" — el silencio aterra.

### Paso 6: Resolución (depende)
Aplicar fix definitivo. Validar en staging si es posible antes de producción.

### Paso 7: All-clear (una vez resuelto)
- Comunicar al cliente.
- Confirmar que todo volvió a métricas normales.
- Pedir confirmación del cliente.

### Paso 8: Postmortem (en 48 h)
Ver sección abajo.

---

## Roles durante un incidente Sev 1

### Incident Commander (IC)
- Es la autoridad final durante el incidente.
- Típicamente el account lead o el CTO JM.
- Toma decisiones de mitigación.
- Comunica al cliente.

### Technical Lead
- Ejecuta el fix.
- Diagnóstica causa raíz.

### Scribe (si hay ≥ 3 personas)
- Documenta la timeline en vivo.
- Toma notas para postmortem.

**Si hay una sola persona, hace los 3 roles pero prioriza mitigación.**

---

## Postmortem — template

Archivo: `/delivery/clients/{{company}}/incidents/{{YYYY-MM-DD}}-{{slug}}.md`

```markdown
# Postmortem — {{Incidente}} — {{Company}}
Severidad: {{Sev 1 / Sev 2}}
Fecha: {{date}}
Autor: {{nombre}}
Status: resolved

## Summary
{{1-2 párrafos de qué pasó y cuál fue el impacto}}

## Timeline (en hora del cliente)
| Hora | Evento |
|---|---|
| 14:32 | Alert dispara: error rate 45% |
| 14:35 | Acknowledged por {{nombre}} |
| 14:40 | War room abierto, cliente avisado |
| 14:52 | Causa raíz identificada: {{...}} |
| 15:08 | Mitigación aplicada (rollback a commit X) |
| 15:15 | Métricas vuelven a baseline |
| 15:30 | All-clear comunicado |

## Impacto
- Volumen afectado: {{N}} transacciones.
- USD de impacto económico: {{}}.
- Usuarios impactados: {{N}}.
- SLAs afectados: {{lista}}.

## Causa raíz
### Inmediata
{{qué detonó el incidente}}

### Subyacente
{{por qué estaba posible que pasara}}

### Sistémica
{{qué proceso / práctica lo permitió}}

## Qué funcionó
-
-

## Qué no funcionó
-
-

## Action items
| # | Acción | Owner | Deadline | Estado |
|---|---|---|---|---|
| 1 | Agregar test para caso X | CTO JM | +7d | open |
| 2 | Alertar antes del threshold | CTO JM | +14d | open |
| 3 | Documentar procedimiento de rollback | PM | +3d | open |

## Regla blameless
Este documento no identifica culpables individuales. El foco es mejorar sistemas, no castigar personas.
```

Postmortem se comparte con cliente si el incidente fue Sev 1 con impacto > 1K USD.

---

## Escalation path

Si el account lead JM no responde:
1. Esperar 15 min.
2. Escalar a CTO JM (Slack + llamada).
3. Esperar 15 min.
4. Escalar a CEO JM (Javier directo).

El cliente siempre tiene un número de emergencia en el runbook.

---

## Runbook del cliente (referenciado)

Cada workstream tiene su `runbook.md` en `/delivery/clients/{{company}}/workstreams/{{name}}/`.

Contenido obligatorio:
- Contactos JM de escalación (nombre, email, teléfono).
- Lista de componentes del sistema con links a sus dashboards.
- Procedimiento de rollback paso a paso.
- Procedimiento de "pausar" el workflow (feature flag).
- FAQ operativo.
- Referencia a este incident-response.md.

---

## Prevención proactiva

Reduce incidentes:
- **Alertas con threshold conservador.** Mejor alerta preventiva que post-mortem.
- **Chaos engineering ligero** (1 vez/trimestre: matar un componente en staging y ver qué pasa).
- **Revisión de incidentes cross-cliente mensual** (patrones comunes entre clientes).
- **Runbook validado** (cada 6 meses, verificar que los pasos funcionen).
- **Rotación de guardias clara** si hay cobertura on-call.

---

## Métricas del proceso de incident response

- Tiempo medio a acknowledge (MTTA): target < 15 min (Sev 1).
- Tiempo medio a mitigate (MTTM): target < 2 h (Sev 1).
- Tiempo medio a resolve (MTTR): target < 24 h (Sev 1).
- # incidentes Sev 1 por cliente por mes: target < 0.5.
- % postmortems completados en < 48 h: target > 90%.
- % action items post-mortem cerrados dentro del deadline: target > 85%.

---

## Comunicación de incidente al cliente — reglas

### Cuándo comunicar
- Sev 1: siempre, dentro de 15 min de acknowledge.
- Sev 2: siempre, dentro de 1 h.
- Sev 3: en el daily / weekly update siguiente.

### Qué NO hacer
- No usar jerga técnica sin explicación.
- No echar culpa al cliente (aunque sea de ellos — primero resolver, después postmortem).
- No prometer ETA que no se cumplirá.
- No dejar a un JR managing la comunicación en Sev 1.

### Qué SÍ hacer
- Decir la verdad.
- Decir qué se está haciendo.
- Decir cuándo viene la próxima update.
- Decir el impacto honesto.

---

## Ver también

- `/maintenance/retainer-model.md` — SLAs por tier
- `/delivery/qa-checklist.md` — prevención durante implementación
- `/delivery/rollout-plan.md` — rollback procedures
