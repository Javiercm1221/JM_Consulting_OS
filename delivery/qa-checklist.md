# QA Checklist — Validación técnica y funcional

Lista completa de verificaciones antes de dar por terminado un workstream. Todo ítem se testea, no se asume.

## Filosofía

> Lo que no testeás, falla en producción un viernes a las 18.

## Cuándo se ejecuta

Al final de cada workstream, antes de pasar de canary a 100% y antes de emitir la factura final.

Responsable: PM JM + 1 reviewer técnico adicional.

---

## Bloque 1 — Funcionalidad

### Casos de uso principales
- [ ] Happy path manual testeado end-to-end.
- [ ] 3 casos edge testeados.
- [ ] 1 caso "basura en input" testeado (prompt injection básico).
- [ ] Salida respeta el formato esperado en 100% de los casos de test.

### Casos de falla controlada
- [ ] Si LLM timeout, el sistema degrada a fallback documentado.
- [ ] Si LLM retorna error 500, el sistema reintenta con backoff exponencial.
- [ ] Si LLM retorna contenido off-topic, el sistema lo marca y escala.
- [ ] Si datos upstream vienen corruptos, el sistema los rechaza con log claro.

### Persistencia
- [ ] Resultados guardados en la tabla correcta.
- [ ] Audit log de cada ejecución (input + output + timestamp + model version).
- [ ] Logs rotados (no crecen infinito).
- [ ] Backups automáticos si hay DB propia.

---

## Bloque 2 — Performance

### Latencia
- [ ] p50 medido y documentado.
- [ ] p95 medido y documentado.
- [ ] p99 medido y documentado.
- [ ] Latencia p95 < target del SOW.

### Throughput
- [ ] Volumen esperado procesable sin cola (o cola dimensionada).
- [ ] Load test a 2× volumen esperado (burst).
- [ ] Comportamiento ante rate limit del LLM documentado.

### Costo
- [ ] Costo por ejecución medido.
- [ ] Costo mensual estimado vs presupuestado en ROI Calculator.
- [ ] Alertas de costo (Slack / email si supera X USD/día).

---

## Bloque 3 — Calidad de output

### Accuracy del modelo
- [ ] Set de evaluación de mínimo 50 casos representativos.
- [ ] Ground truth validado por humano experto (operador cliente).
- [ ] Accuracy ≥ umbral del SOW.
- [ ] Matriz de confusión armada (para clasificación).
- [ ] F1 score calculado.
- [ ] Falsos positivos analizados (costo de cada uno).
- [ ] Falsos negativos analizados (costo de cada uno).

### Robustez
- [ ] Testeado con inputs en mayúsculas, minúsculas, con errores ortográficos.
- [ ] Testeado con inputs muy largos (beyond context window).
- [ ] Testeado con inputs muy cortos.
- [ ] Testeado en idiomas secundarios si el caso lo requiere.

### Bias
- [ ] Revisión de bias obvio (género, origen, etc.) si aplica al caso.
- [ ] Notas de limitaciones documentadas.

---

## Bloque 4 — Seguridad

### Secretos y credenciales
- [ ] API keys fuera del código (variables de entorno / vault).
- [ ] Rotación de keys documentada y agendada.
- [ ] Accesos mínimos (principio de menor privilegio).
- [ ] Audit log de accesos a sistemas sensibles.

### Data sensible
- [ ] PII no logueada en prompts guardados.
- [ ] PII no logueada en respuestas guardadas (mask / redact).
- [ ] DPA firmado con LLM provider.
- [ ] Si aplica HIPAA / GDPR / etc., cumplimiento validado.

### Prompt injection
- [ ] System prompt protegido (no expuesto en errores).
- [ ] User input validado / sanitizado.
- [ ] Test de "ignore previous instructions" passed.

### Runtime
- [ ] Rate limiting activo (si es endpoint público).
- [ ] Timeouts configurados.
- [ ] Circuit breaker / fallback implementado.

---

## Bloque 5 — Observabilidad

### Logs
- [ ] Logs estructurados (JSON).
- [ ] Niveles (debug, info, warn, error) usados correctamente.
- [ ] Correlation ID en cada request.
- [ ] Logs accesibles al equipo JM + operador cliente designado.

### Métricas
- [ ] Dashboard con KPIs del workstream activo.
- [ ] Métricas técnicas: latency, error rate, throughput.
- [ ] Métricas de negocio: la que define el outcome.
- [ ] Refresh rate < 15 min (ideal near real-time).

### Alertas
- [ ] Alerta si error rate > X%.
- [ ] Alerta si latency p95 > Y ms por Z minutos.
- [ ] Alerta si volumen drop > 50% vs baseline.
- [ ] Alerta si costo diario > Z USD.
- [ ] Canal de alertas (Slack / email / PagerDuty) definido y testeado.

---

## Bloque 6 — Operación

### Runbook
- [ ] Documento escrito describiendo qué hacer si falla.
- [ ] Contactos de escalación listados.
- [ ] Tiempos de respuesta esperados.
- [ ] Procedimiento de rollback paso a paso.
- [ ] Procedimiento de recuperación de data si aplica.

### Handoff operativo
- [ ] Operador cliente capacitado (video 15 min + sesión en vivo).
- [ ] FAQ inicial documentado.
- [ ] Canal de soporte abierto con SLA claro.
- [ ] Persona backup identificada.

### Mantenimiento
- [ ] Frecuencia de evaluación de accuracy agendada (semanal / mensual).
- [ ] Plan de re-training del modelo si aplica.
- [ ] Plan de actualización del system prompt documentado.

---

## Bloque 7 — Documentación

### Técnica
- [ ] README en el repo con setup local.
- [ ] Arquitectura diagramada (Mermaid / draw.io).
- [ ] API docs si hay endpoints (OpenAPI).
- [ ] Variables de entorno documentadas (.env.example).
- [ ] Dependencias listadas con versiones.

### Usuario final
- [ ] Manual del operador (PDF).
- [ ] Video walkthrough (5-15 min).
- [ ] FAQ del operador.

### Compliance / legal
- [ ] DPA firmado con cliente.
- [ ] Lista de proveedores terceros usados (LLM, vector DB, etc.).
- [ ] Términos de uso / limitaciones comunicados por escrito.

---

## Bloque 8 — Financiero / comercial

- [ ] Costo real año 1 actualizado en ROI Calculator.
- [ ] Invoice final emitida según SOW.
- [ ] Signoff del sponsor firmado (email explícito válido).
- [ ] Case study (interno) redactado (1 página).
- [ ] Feedback del cliente solicitado (NPS + 2 preguntas abiertas).

---

## Bloque 9 — Handoff a Mantenimiento

- [ ] Retainer mensual firmado (si aplica).
- [ ] Scope del retainer claro (ver `/maintenance/retainer-model.md`).
- [ ] Transferencia de propiedad intelectual clarificada.
- [ ] Owner JM asignado para el mantenimiento.
- [ ] Primera monthly review agendada.

---

## Formato de ejecución

### Opción A — Checklist manual
Copiar esta lista a `/delivery/clients/{{company}}/workstreams/{{workstream}}/qa.md` y tickear en Paperclip.

### Opción B — Automated checks
Donde sea posible, automatizar:
- Tests unitarios / integración corren en CI.
- Load tests scripted (k6, Locust).
- Linters y security scanners (bandit, Semgrep).
- Pipelines de evaluación de accuracy automáticos.

Mantener la checklist manual incluso cuando hay automation — hay cosas que solo un humano revisa (documentación, handoff).

---

## Criterio de cierre

Workstream se cierra solo cuando:
1. **100% de items críticos** (Bloques 1-5) marcados.
2. **≥ 90% de items del resto** marcados.
3. Sponsor firma signoff.

Items no críticos pendientes van a backlog con owner y deadline.

---

## Ver también

- `/delivery/quick-wins-sprint.md` — contexto del sprint
- `/delivery/implementation-scope.md` — scope referencia
- `/delivery/rollout-plan.md` — plan de rollout al 100%
- `/maintenance/incident-response.md` — qué hacer si falla post-prod
