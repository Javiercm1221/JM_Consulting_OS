# Approvals Policy — Qué requiere aprobación humana

Define claramente qué acciones pueden ejecutar los agentes de forma autónoma, qué requiere aprobación del CEO agent, y qué requiere aprobación de Javier como humano en el loop.

## Principio base

Los agentes son rápidos pero no son el owner. Todo lo que genera compromiso externo (con clientes, legal, financiero), que afecta el stack core, o que toca cambios mayores de rumbo requiere aprobación humana explícita.

---

## Tres niveles de approval

### Nivel 0 — Autónomo
El agente ejecuta sin preguntar. Loggea la acción en Paperclip.

### Nivel 1 — CEO agent approval
El agente propone, el CEO agent aprueba o rechaza. El CEO puede escalar a Javier si duda.

### Nivel 2 — Javier approval (human in the loop)
El agente propone, espera aprobación explícita de Javier antes de ejecutar. No hay atajos.

---

## Matriz de approvals

### Acciones comerciales (sales / pricing)

| Acción | Nivel | Notas |
|---|---|---|
| Enviar email outbound de campaña estándar | 0 | Dentro de templates aprobados |
| Responder a inbound lead con scripts estándar | 0 | — |
| Agendar discovery call | 0 | — |
| Customizar email fuera del template | 1 | Review del CRO agent |
| Enviar propuesta de audit (10K) | 1 | CEO aprueba |
| Enviar propuesta de implementación | 2 | Javier firma |
| Ofrecer descuento > 10% | 2 | Javier aprueba |
| Extender trial / freebie | 1 | CEO aprueba |
| Cambiar pricing base | 2 | Javier + COO |
| Contratar cliente nuevo (firma SOW) | 2 | Javier firma |

---

### Acciones financieras

| Acción | Nivel | Notas |
|---|---|---|
| Emitir factura de retainer / milestone | 0 | Según SOW firmado |
| Enviar recordatorio de pago | 0 | Hasta 2 recordatorios |
| Pausar servicio por impago | 2 | Javier aprueba |
| Gasto nuevo recurrente < 100 USD/mes | 1 | COO aprueba |
| Gasto nuevo recurrente 100-1000 USD/mes | 1 | CEO + COO aprueban |
| Gasto nuevo recurrente > 1K USD/mes | 2 | Javier aprueba |
| Gasto one-time > 500 USD | 2 | Javier aprueba |
| Emitir reembolso a cliente | 2 | Javier aprueba |
| Pagar contractor | 1 | COO ejecuta con SOW firmado |
| Cambio de banco / stripe / wise | 2 | Javier aprueba |

---

### Acciones técnicas

| Acción | Nivel | Notas |
|---|---|---|
| Crear branch / PR en código JM interno | 0 | — |
| Merge a main de código JM interno | 1 | CTO review / self-review |
| Commit a código de cliente (branch) | 0 | — |
| Merge a main en código de cliente | 2 | Javier + account lead |
| Deploy a staging del cliente | 1 | CTO aprueba |
| Deploy a prod del cliente | 2 | Javier + sponsor cliente |
| Cambio de stack core de JM | 2 | Javier |
| Subir un nuevo n8n workflow JM | 1 | CTO self-review |
| Subir un nuevo workflow al cliente | 2 | Javier + sponsor |
| Ejecutar script de migración de datos | 2 | Javier + sponsor |
| Borrar data productiva | 2 | Javier + sponsor + backup confirmado |
| Rotar credenciales | 1 | COO aprueba |
| Acceso nuevo a 1Password | 2 | Javier aprueba |
| Cambio de modelo LLM usado en delivery | 1 | CTO aprueba + notificar CEO |
| Aumento de API budget > 20% | 2 | Javier |

---

### Acciones de contenido / público

| Acción | Nivel | Notas |
|---|---|---|
| Publicar post LinkedIn estándar | 1 | CEO review |
| Publicar post con data de cliente | 2 | Javier + cliente (escrito) |
| Enviar newsletter | 1 | CEO review |
| Publicar case study | 2 | Javier + cliente |
| Cambio de copy en landing page | 1 | CEO + CMO |
| Cambio de posicionamiento de la firma | 2 | Javier |
| Responder críticas públicas | 2 | Javier |
| Webinar / evento público de la firma | 2 | Javier |

---

### Acciones de personas / HR

| Acción | Nivel | Notas |
|---|---|---|
| Onboarding contractor existente a nuevo proyecto | 1 | COO + CEO |
| Contratar contractor nuevo | 2 | Javier firma contrato |
| Offboarding contractor | 2 | Javier |
| Cambio de responsabilidades / scope | 2 | Javier |
| Crear agente nuevo (rol nuevo) | 2 | Javier |
| Dar de baja agente existente | 2 | Javier |
| Cambio de instructions.md de agente existente | 1 | CEO aprueba |

---

### Acciones con datos de clientes

| Acción | Nivel | Notas |
|---|---|---|
| Leer datos del cliente ya autorizados en SOW | 0 | — |
| Leer datos no cubiertos en SOW | 2 | Javier + sponsor cliente |
| Copiar datos del cliente a sistemas JM | 2 | Javier + sponsor (DPA) |
| Compartir insight agregado de cliente con otros agentes | 1 | CEO aprueba |
| Usar data del cliente para training de modelo JM | 2 | Javier + cliente (legal) |
| Purgar data del cliente post-contrato | 1 | COO ejecuta según DPA |

---

### Acciones legales / regulatorias

| Acción | Nivel | Notas |
|---|---|---|
| Firmar cualquier contrato | 2 | Javier (único firmante) |
| Enviar NDA propio a prospect | 1 | COO usa template |
| Aceptar NDA del cliente | 2 | Javier + legal externo |
| Responder a subpoena / legal notice | 2 | Javier + abogado |
| Acuerdo de data processing (DPA) | 2 | Javier + abogado |
| Cambio de términos de servicio públicos | 2 | Javier + abogado |

---

### Acciones de crisis / escalamiento

| Acción | Nivel | Notas |
|---|---|---|
| Declarar incidente Sev 1 | 0 | Cualquier agente puede |
| Pausar servicio en un incidente | 1 | CTO + CEO |
| Comunicación pública sobre un incidente | 2 | Javier |
| Escalation legal por cliente | 2 | Javier + abogado |
| Terminación anticipada de contrato con cliente | 2 | Javier |
| Pausar cliente problemático | 2 | Javier |

---

## Formato del request de approval

Cuando un agente necesita approval, crea un issue en Paperclip con:

```
Título: [APPROVAL] <Acción propuesta>

Tipo: Nivel 1 (CEO) | Nivel 2 (Javier)

Contexto:
- Qué se quiere hacer
- Por qué ahora
- Cliente / proyecto afectado

Impacto si se aprueba:
- $ / tiempo / riesgo

Impacto si NO se aprueba:
- Oportunidad perdida / bloqueo

Alternativas consideradas:
- A: ...
- B: ...

Recomendación del agente:
- [aprobar / rechazar / esperar más data]

Deadline de decisión:
- [fecha y hora específica]
```

---

## SLA de decisión

| Nivel | Tiempo máximo de respuesta |
|---|---|
| Nivel 1 (CEO agent) | 4 h durante ventana laboral |
| Nivel 2 (Javier) | 24 h durante ventana laboral |
| Nivel 2 urgente (Sev 1 / cliente enojado) | 1 h cualquier horario |

Si el SLA se vence sin decisión:
- Nivel 1: se marca como "bloqueado por CEO agent", se espera.
- Nivel 2: se envía reminder a Javier; nunca se ejecuta sin su OK.

---

## Delegación temporal (vacations / off)

Cuando Javier está off > 3 días:
1. Javier pre-aprueba un scope en un issue (`[PRE-APPROVED] vacations window X-Y`).
2. Durante la ventana, CEO agent puede autorizar Nivel 2 dentro del scope.
3. Nada fuera del scope se ejecuta; espera el regreso.
4. Ejemplo de scope pre-aprobado: "enviar propuestas < 15K, aprobar gastos < 500 USD, responder clientes activos, no firmar contratos nuevos".

---

## Log de approvals

Todos los approvals quedan registrados en:
- Paperclip (issue con decisión).
- Notion / Drive: `/company/approval_log.md` con fecha, agente, acción, nivel, decisión, razón.

COO audita el log trimestralmente:
- Porcentaje de requests aprobados vs rechazados.
- Tiempo medio de decisión.
- Requests que debieron ser autónomos pero fueron pedidos (mejora de instrucciones).
- Acciones autónomas que debieron requerir approval (riesgo a mitigar).

---

## Casos especiales

### Emergencia genuina (incendio)
Si hay riesgo real e inmediato (Sev 1 cliente, dinero en riesgo) y Javier no responde en < 1 h:
- CEO agent puede autorizar mitigación temporal (rollback, freeze, comunicación básica al cliente).
- NO puede firmar contratos, gastar dinero nuevo, ni cambiar pricing.
- Todo debe documentarse y revisarse con Javier < 24 h después.

### Cliente pide algo fuera de SOW
- Agente responde: "déjame confirmar con el equipo y te vuelvo hoy / mañana".
- Crea issue de approval.
- Nunca commit en la llamada sin check.

### Javier aprueba algo "a mano" fuera de Paperclip
- Quien recibió la aprobación la loggea en Paperclip con captura o quote.
- Si no queda loggeada, no se ejecuta.

---

## Anti-patterns

- Pedir approval para todo (genera friction, deja a Javier de cuello de botella).
- Saltear approval "porque era obvio" (rompe el log y la confianza).
- Approvals verbales sin log (no existen).
- Pre-aprobaciones genéricas sin scope ("puedes hacer lo que quieras").
- Escalar a Javier lo que el CEO agent debería decidir solo.

---

## Ver también

- `/paperclip/tool-access-matrix.md`
- `/paperclip/heartbeat-policy.md`
- `/paperclip/ceo-instructions.md`
- `/paperclip/coo-instructions.md`
- Todos los `*-instructions.md`.
