# Stakeholder Interviews — Entrevistas a ejecutivos

Plantilla para entrevistar a C-level y líderes de área. Objetivo: obtener la visión estratégica y validar outcomes.

## Duración

45-60 minutos por ejecutivo.

## Participantes típicos

- CEO / Managing Partner (siempre).
- COO / Director of Operations.
- CFO / Finance Lead.
- CRO / VP Sales.
- CTO / Head of Tech.
- Head of CS / Customer Success.

## Método de entrevista

### Preparación (30 min antes)
1. Leer LinkedIn del ejecutivo.
2. Revisar su discurso público (podcasts, entrevistas, eventos).
3. Leer materiales internos que ya compartieron.
4. Preparar 1-2 observaciones específicas para el rapport.

### Apertura (5 min)
```
"Gracias por el tiempo. Lo que quiero entender es tu visión del negocio,
qué está funcionando, qué no, y dónde sentís que hay palanca sin usar.
Al final te voy a preguntar dónde creés que la IA puede jugar, pero
quiero primero escuchar tu lectura sin filtro."
```

### Set expectations
- "Esto es confidencial. Lo que me digas no va a otros entrevistados sin tu OK."
- "Voy a tomar notas. ¿Podemos grabar para no perder nada?"
- "Al final te muestro un resumen de 5 puntos."

---

## Bloque 1 — Visión de negocio (15 min)

1. Contame el negocio en 3 frases, como si yo fuera un inversor.
2. ¿Cuál es la ventaja competitiva real?
3. ¿Qué competidor te preocupa y por qué?
4. ¿Qué métricas mirás todos los días?
5. ¿Qué métricas mirás mensualmente?
6. ¿Dónde está el crecimiento el próximo año?
7. ¿Qué es lo que más te desvela?

---

## Bloque 2 — Operación actual (15 min)

8. ¿Qué proceso operativo hoy sentís que es tu mayor cuello de botella?
9. ¿Qué te impidió resolverlo hasta ahora?
10. ¿Dónde sentís que el equipo pierde tiempo en cosas que no agregan valor?
11. ¿Qué hacen tus competidores mejor que ustedes en operación?
12. ¿Qué software usan y cuáles te dan más frustración?
13. ¿Qué handoff entre áreas es el más problemático?
14. ¿Dónde hay re-trabajo recurrente?

---

## Bloque 3 — Palancas y oportunidad (15 min)

15. Si tuvieras una varita mágica para arreglar una sola cosa de la operación, ¿qué sería?
16. ¿Dónde sentís que hay dinero enterrado?
17. ¿Qué procesos, si se hicieran 10× más rápido, cambiarían el negocio?
18. ¿Qué tarea de tu gente hace que pensás "esto no lo debería estar haciendo una persona"?
19. ¿Dónde creés que la IA puede jugar y dónde creés que NO?
20. ¿Qué has probado antes y no funcionó? ¿Por qué?

---

## Bloque 4 — Personas y cambio (10 min)

21. ¿Quién en tu equipo está más abierto al cambio tecnológico?
22. ¿Quién podría oponerse y por qué?
23. ¿Cómo es la comunicación interna sobre cambios de herramientas?
24. ¿Tenés a alguien técnico interno que pueda colaborar con la implementación?
25. ¿Qué has aprendido de implementaciones anteriores (buenas o malas)?

---

## Bloque 5 — Restricciones y éxito (5 min)

26. ¿Hay líneas rojas? (data sensible, clientes que no se tocan, compliance)
27. ¿Cuál es el nivel de inversión que no necesita aprobación del board?
28. ¿Qué resultado a 12 meses sería un éxito rotundo?
29. ¿Qué sería fracaso?
30. ¿Con qué frecuencia querés status update durante el audit?

---

## Checklist post-entrevista

- [ ] Agradecer por email en < 2 h.
- [ ] Resumen de 5 bullets al entrevistado para validación.
- [ ] Cargar transcript completo en `/delivery/clients/{{company}}/interviews/{{name}}.md`.
- [ ] Extraer: 3 dolores, 2 oportunidades, 1 riesgo → tabla consolidada.
- [ ] Actualizar business map con data nueva.
- [ ] Si aparece tarea candidata, agregar al task map.

---

## Plantilla de notas (1 por entrevistado)

```markdown
# Entrevista: {{name}} ({{role}}) — {{company}}
Fecha: {{date}}
Duración: {{min}}
Grabación: {{link si aplica}}

## Visión del negocio
- Ventaja competitiva:
- Competidor que preocupa:
- Growth driver 2026:

## Dolor operativo
1.
2.
3.

## Oportunidades sugeridas
1.
2.

## Restricciones
-

## Stakeholders mencionados
- {{nombre}} — {{por qué relevante}}

## Outcomes propuestos
-

## Quotes útiles para deck
> "..."

## Follow-ups
- [ ]
```

---

## Reglas durante la entrevista

- **Escuchar 80, hablar 20.**
- **Nunca pitchar en la primera entrevista ejecutiva.**
- **Si aparece una pista de dolor, cavar.** ("¿A qué costo? ¿Cuánta gente? ¿Hace cuánto?")
- **Tomar números siempre.** Si dice "mucho tiempo", preguntar cuánto.
- **Anotar nombres.** Cada persona mencionada es una entrevista potencial.
- **Cerrar con "¿a quién más debería hablar?"**

---

## Anti-patterns

- Preguntar sobre IA en los primeros 30 min → sesga al entrevistado.
- Aceptar "mucho" / "poco" sin cuantificar.
- No validar el resumen → da lugar a malos entendidos que explotan en el deck final.
- Entrevistas sin agenda previa compartida.

---

## Referencias cruzadas

- Paso siguiente: `/audit/employee-interviews.md`
- Framework: `/audit/roi-first-framework.md`
- Técnica: `/audit/yesterday-morning-method.md`
