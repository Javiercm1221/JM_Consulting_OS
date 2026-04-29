# Incident Response — CTO

## Severidad

| Nivel | Definición | Ejemplo |
|---|---|---|
| Sev 1 | Sistema productivo del cliente caído o produciendo outputs incorrectos en > 20% de casos | Workflow enviando emails erróneos, CRM corrupto, API caída |
| Sev 2 | Degradación significativa (latencia > 3x, accuracy bajó > 15%) pero sin caída total | Respuestas lentas, mayor tasa de escalación a humano |
| Sev 3 | Issue menor o cosmético, no impacta al cliente | Bug en dashboard, log faltante, alerta falsa |

## SLA de respuesta

| Severidad | MTTA (tiempo a primer ack) | MTTR (tiempo a resolución) |
|---|---|---|
| Sev 1 | < 30 min (cualquier horario) | < 4 horas |
| Sev 2 | < 2 horas (horario laboral) | < 24 horas |
| Sev 3 | < 24 horas (horario laboral) | < 72 horas |

## Protocolo Sev 1

1. **Ack inmediato** en Slack #alerts-prod: "Confirmo Sev 1 en [cliente]. Investigando."
2. **Rollback** si hay rollback disponible — no investigar con el sistema caído.
3. **Notificar al cliente** en < 30 min (template abajo).
4. **Escalar al CEO** si no hay resolución en 1 hora.
5. **Escalar a Javier** si el CEO no puede resolver.
6. **Post-mortem** en < 48 h post-resolución.

## Template de comunicación al cliente (Sev 1)

```
Asunto: Actualización — [nombre del sistema]

Hola [nombre],

Detectamos un problema en [descripción breve del sistema] 
que puede estar afectando [descripción del impacto].

Estamos trabajando en la resolución. ETA inicial: [tiempo].

Actualizaciones cada 30 minutos hasta resolver.

Tomás / JM Consulting
```

## Post-mortem (obligatorio para Sev 1)

Formato a completar en < 48 h post-resolución:

```
## Post-mortem — [nombre sistema] — [fecha]

**Duración del incidente:** [desde] → [hasta]
**Impacto:** [qué afectó, cuántos usuarios/operaciones]
**Causa raíz:** [qué falló exactamente]
**Timeline:**
- [hora] — [qué pasó]
- [hora] — [acción tomada]
- [hora] — [resolución]

**Qué funcionó bien:**
-

**Qué falló en el proceso:**
-

**Acciones preventivas (con owner y deadline):**
1.
2.
```
