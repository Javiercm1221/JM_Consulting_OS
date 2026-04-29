# Glosario — JM Consulting

Términos internos que usan los agentes. Si no está acá, usar lenguaje estándar.

---

## Términos de negocio

**ROI-first framework**
Metodología de la firma: antes de recomendar cualquier solución tecnológica, se cuantifica el problema en USD/año. Ninguna oportunidad llega a la Opportunity Matrix sin número de dólares asociado.

**AI Opportunity Audit**
Producto de entrada de JM Consulting. Diagnóstico de 2 semanas que entrega 8 entregables (ver `pricing_service_ladder.md`). Precio orientativo: 5K-50K USD según segmento.

**Service Ladder**
Los 5 peldaños de servicios de JM Consulting: (1) AI Audit → (2) Lead Gen Engine → (3) Quick Wins Sprint → (4) Strategic Implementation → (5) Retainer.

**ICP (Ideal Customer Profile)**
Perfil del cliente ideal. Para property management: empresa con 15M+ ARR, 100+ propiedades, 10+ empleados en roles operativos.

**Nicho actual**
Property management (gestión de propiedades). Mercado prioritario hasta nueva autorización de Javier.

**Pipeline**
Conjunto de oportunidades comerciales en distintas etapas del proceso de venta (lead → discovery → propuesta → audit → implementación → retainer).

**Retainer**
Acuerdo de mantenimiento mensual. Tres tiers: Starter (2K/mes), Pro (5K/mes), Scale (10K/mes).

---

## Términos de auditoría

**Yesterday morning technique**
Técnica de entrevista: se le pide al entrevistado que describa en detalle lo que hizo "ayer a la mañana". Permite descubrir pasos ocultos, ineficiencias y procesos no documentados que el entrevistado no menciona espontáneamente.

**Business map**
Mapa de los tres flujos del negocio del cliente: acquisition (cómo consigue clientes), delivery (cómo entrega su servicio) y support (cómo da soporte postventa).

**Task map**
Descomposición de microtrabajos dentro de cada proceso del business map. Nivel de granularidad: acciones individuales que puede realizar un empleado o un agente.

**Opportunity matrix**
Matriz 2x2 de impacto vs esfuerzo que clasifica oportunidades de automatización en: Quick Wins, Big Swings, Nice-to-Have, y Deprioritize.

**Quick wins**
Oportunidades con alto impacto y bajo esfuerzo. Se ejecutan en el Quick Wins Sprint. Criterio: sí a las 4 preguntas del filtro de priorización.

**Big swings**
Oportunidades de alto impacto pero alto esfuerzo. Se ejecutan en Strategic Implementation tras validar quick wins.

**Filtro de priorización (4 preguntas)**
Una oportunidad pasa si responde SÍ a las 4:
1. ¿El input es estructurado?
2. ¿El output es predecible?
3. ¿La decisión sigue reglas?
4. ¿Se repite con frecuencia?

**Haircut conservador**
Ajuste del 20% aplicado a todos los cálculos de ROI antes de presentarlos al cliente. Objetivo: mantener credibilidad y no sobreprometer.

**Outcome**
Resultado de negocio medible que el cliente quiere lograr. Formato: "estado actual → estado objetivo → delta". Ejemplo: "Tiempo de respuesta a leads: 4h → 15 min → ahorro de 40 h/semana de equipo."

---

## Términos operativos

**Paperclip**
Plataforma de orquestación multi-agente auto-hospedada donde viven y se coordinan los 6 agentes de JM Consulting.

**Heartbeat**
Política de cuándo se activa cada agente. Tres modos: Rhythmic (calendario fijo), Event-driven (disparado por un evento), On-call (disponible en ventana horaria).

**Approval (Nivel 0/1/2)**
Sistema de aprobaciones. N0: el agente actúa solo. N1: el CEO Agent aprueba. N2: Javier aprueba.

**Issue**
Unidad de trabajo en Paperclip. Todo task, approval request o entregable se trackea como un issue.

**Pod (client pod)**
Espacio de trabajo en Paperclip para un cliente específico. Agrupa agentes relevantes, documentos, heartbeat y comunicaciones del cliente.

**Sprint**
Ciclo de implementación de 4 semanas. Fases: setup → pilot → canary rollout → 100% + métricas.

**Sev 1 / Sev 2**
Niveles de incidente. Sev 1: impacto crítico en producción del cliente, requiere respuesta en < 30 min. Sev 2: impacto parcial, respuesta en < 4 h.

**SOW (Statement of Work)**
Documento contractual que define el alcance, entregables, precios y plazos de un engagement. Solo Javier puede firmarlo.

**DPA (Data Processing Agreement)**
Acuerdo de procesamiento de datos requerido cuando la firma accede a datos de clientes. Requiere aprobación de Javier + abogado.

---

## Términos de outbound / CRO

**Instantly**
Plataforma de cold email outbound. Maneja warmup, envío y follow-ups.

**Apollo / Clay**
Herramientas de lead enrichment y prospecting. Apollo para datos de contacto, Clay para enriquecimiento avanzado.

**HeyReach**
Plataforma de outreach en LinkedIn.

**Positive reply**
Respuesta de un prospect que indica interés real en una llamada o más información. Requiere respuesta del CRO en < 60 min.

**Discovery call**
Primera llamada de 30-45 min con un prospect calificado. Objetivo: confirmar ICP, identificar pain points y agendar siguiente paso.

**Shown appointment**
Reunión de discovery donde el prospect efectivamente asistió. Métrica de performance del Lead Gen Engine.

---

## Agentes (nombres internos)

| Rol | Nombre | Responsabilidad |
|---|---|---|
| CEO Agent | Alex | Coordinación general, prioridades, aprobaciones N1 |
| CRO Agent | Sol | Pipeline, outbound, cierre |
| Head of AI Audit | Andrés | Entregas de auditoría ROI-first |
| CTO Agent | Tomás | Implementaciones técnicas, n8n, delivery |
| COO Agent | Clara | Operaciones internas, finanzas, procesos |
| CMO Agent | Mei | Contenido, branding, thought leadership |
| Client Success Lead | Luca | Retención, MBRs, retainers activos |
