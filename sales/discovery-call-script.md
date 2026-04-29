# Discovery Call Script

Script para la primera llamada con un prospecto. Objetivo: calificar y cerrar la venta del audit (no del proyecto grande).

## Duración

20-30 minutos.

## Estructura (bloques de tiempo)

| Bloque | Tiempo | Objetivo |
|---|---|---|
| 1. Apertura | 2 min | Romper hielo + set expectations |
| 2. Diagnóstico | 10 min | Dolor, dinero, contexto |
| 3. Validación | 5 min | Cualificar presupuesto y timing |
| 4. Pitch del audit | 5 min | Presentar el producto de entrada |
| 5. Cierre | 5 min | Siguiente paso concreto |

## Bloque 1 — Apertura

```
"Gracias por el tiempo, {{firstName}}. Tenemos 25 minutos.
Lo que quiero hacer es entender qué está pasando en {{company}} hoy
en operaciones, dónde sienten que se escapan horas o dinero, y al final
te cuento qué hacemos nosotros y si tiene sentido seguir conversando. ¿Te parece?"
```

Regla: **no pitchar en los primeros 15 minutos.**

## Bloque 2 — Diagnóstico (el núcleo)

### Preguntas iniciales

1. Contame en 2 minutos qué hace {{company}} y cuál es tu rol.
2. ¿Cuántas personas trabajan en operaciones/back office?
3. ¿Qué procesos son los más críticos para ustedes hoy?

### Preguntas de dolor (orientadas a dinero)

4. ¿Cuál es el problema más caro que tenés hoy?
5. ¿Qué cosa, si la resolviéramos, mejoraría revenue?
6. ¿Dónde sabés que perdés dinero y todavía no lo arreglaste?
7. ¿Qué tarea consume horas valiosas del equipo?
8. ¿Qué software usan y cuáles les generan más frustración?
9. ¿Qué problema arreglarían con una varita mágica?

### Yesterday morning technique

10. Contame ayer a la mañana. ¿Qué hiciste primero?
11. ¿Después qué?
12. ¿Y luego?

Esto revela pasos ocultos, fricciones, duplicaciones.

### Preguntas de éxito

13. ¿Qué se vería como éxito si estos problemas se resolvieran?
14. ¿Qué métrica cambiaría y en cuánto?

## Bloque 3 — Validación

Preguntas para calificar si vale la pena avanzar.

1. ¿Quién más estaría involucrado en una decisión de este tipo?
2. ¿Tienen presupuesto asignado para iniciativas tecnológicas este año?
3. ¿En qué orden de magnitud? (ayuda a que suelten el rango)
4. ¿Han intentado algo similar antes? ¿Cómo les fue?
5. ¿Hay algún trigger puntual que te lleve a mirar esto ahora?

### Criterios de calificación

Tiene que haber al menos 3 sí:

- ☐ Dolor claro y económicamente cuantificable.
- ☐ Sponsor ejecutivo en la llamada o identificable.
- ☐ Budget > 5K USD disponible.
- ☐ Timing dentro de 90 días.
- ☐ Stack tecnológico razonable (CRM/ERP moderno).

## Bloque 4 — Pitch del audit (no del proyecto grande)

**Qué NO hacer:** hablar de chatbots, n8n, agentes, Paperclip. Todavía.

**Qué SÍ hacer:**

```
"Basado en lo que me contás, lo que encuentro en empresas como {{company}} es
entre 150K y 400K al año de fuga por [tareas mencionadas]. Para darte un número
real para tu operación, lo que hacemos es un audit ROI-first de 2 semanas.

Qué incluye:
- 5-10 entrevistas con tu equipo
- Mapa completo de procesos
- Identificación de las 10 oportunidades con más upside
- ROI calculado para cada una
- Roadmap de 90 días con quick wins primero
- Deck ejecutivo para presentar al board

Pricing: 10K flat. Si después contratás implementación, el 100% se acredita.

En 2 semanas tenés claridad sobre dónde vale la pena invertir y dónde no.
No te vendemos nada que no tenga número."
```

## Bloque 5 — Cierre

Opciones:

**Cierre directo (preferido):**
```
"Por lo que vi en la llamada, claramente hay fugas que vale la pena cuantificar.
¿Arrancamos con el audit? Te mando la propuesta hoy con dos fechas de kickoff."
```

**Cierre con stakeholders adicionales:**
```
"¿Quién más tendría que ver la propuesta para aprobar el audit?
Puedo sumarte a {{name}} en la próxima llamada y presentamos juntos."
```

**Cierre con calendarización:**
```
"Te paso propuesta hoy. ¿Te pareció si agendamos 30 min el {{day}} para
decidir go/no-go y ajustar scope si hace falta?"
```

## Objeciones comunes → referir a objection-handling.md

## Post-call checklist

- [ ] Enviar resumen por email en < 2 h
- [ ] Enviar propuesta en < 24 h
- [ ] Cargar en CRM con stage "audit proposed"
- [ ] Definir próximo touchpoint en calendario
- [ ] Agregar 1-2 insights del call al ICP doc
- [ ] Si hay señales de urgencia, marcar HOT

## Red flags durante el call

Si aparecen 2+, descalificar con elegancia:

- No quieren dar números ni estimados.
- Dicen "ya probamos IA y no funcionó" sin detallar.
- El decisor "no estaba disponible hoy".
- Preguntan por "caso de estudio gratis" antes que por el producto.
- Equipo < 5 personas.
- Sin CRM / sin stack digital.
