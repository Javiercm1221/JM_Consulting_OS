# Yesterday Morning Method

Técnica de entrevista para **descubrir el trabajo real**, no el trabajo teórico.

## Origen y por qué funciona

Cuando se pregunta "¿cómo haces X?", el entrevistado responde una versión idealizada del proceso. Cuando se pregunta "¿qué hiciste ayer a las 9:15?", responde con verdad: pausas, fricciones, ruido, handoffs lentos.

La memoria de 24 horas es precisa en detalle, difícil de dramatizar y rápida de reconstruir.

## Cuándo usarla

- Con operadores (siempre).
- Con líderes de primera línea (usualmente).
- Con C-level (cuando hay señal de que no conoce la operación al detalle).

## Cuándo NO usarla

- Si el entrevistado tuvo un día atípico ayer (vacaciones, evento especial).
  - Alternativa: "Contame el lunes pasado."
- Si trabaja en turnos rotativos y ayer fue su día libre.
  - Alternativa: "Contame tu último día de trabajo."

---

## Estructura de la sesión (30 min)

### Pre-apertura (2 min)
```
"Quiero hacer un ejercicio específico. Te voy a pedir que me cuentes tu
mañana de ayer paso a paso, lo más detallado posible. No es test, no
necesitás prepararte. Arranca cuando te parezca."
```

### Ejecución (20 min)
- El entrevistado narra libremente 2-3 minutos.
- A partir de ahí, el entrevistador **interrumpe SOLO con preguntas de detalle**, nunca con opiniones.

### Cierre (8 min)
- Síntesis de tareas mapeadas.
- Preguntas de profundización.

---

## Las 7 preguntas de profundización

Cada vez que el entrevistado nombra una actividad, aplicar hasta 7 preguntas:

1. **¿Cuánto tardaste?**
2. **¿De dónde sacaste el input?**
3. **¿A dónde mandaste el output?**
4. **¿Qué hubiera pasado si no estabas vos?**
5. **¿Qué pasa cuando hay un error?**
6. **¿Cuántas veces por semana haces eso?**
7. **¿Alguien más lo hace de otra manera?**

No hace falta hacer las 7 todas las veces. Suficiente con 2-3 por tarea.

---

## Ejemplo de narrativa extraída

### Output crudo del entrevistado
```
Entrevistado: "Llegué a las 8:30, abrí el mail, tenía 28 correos. Los
fui leyendo, algunos los contesté y otros los tiré en la carpeta de
pendientes. Después abrí el CRM, había 14 leads nuevos de la noche,
los revisé uno por uno, a 4 los derivé a María porque eran de su zona,
a 3 los puse en status 'no califica'. Después me llamó Ramón preguntando
por el reporte de la semana pasada, se lo armé a mano en Excel porque
el sistema no lo exporta, tardé como 40 min. Recién ahí desayuné."
```

### Tareas extraídas (agregar a task map)

```
| Task | Frec/sem | Tiempo/vez | Sistema | Handoff | Valor hora | Costo/sem |
|---|---|---|---|---|---|---|
| Triage de inbox | 5 | 30 min | Gmail | - | $25 | $62 |
| Lectura y ruteo de leads | 5 | 20 min | CRM | → María | $25 | $42 |
| Calificación manual de leads | 5 | 15 min | CRM | - | $25 | $31 |
| Armado manual de reporte semanal | 1 | 40 min | Excel | → Ramón | $25 | $17 |
```

### Señales capturadas
- Inbox triage → candidato a clasificación automática.
- Ruteo de leads → rules-based automation simple (no IA).
- Reporte semanal manual → query + scheduled report (no IA, pero alto impacto).
- Handoff a María → depende de disponibilidad humana.

---

## Reglas del entrevistador

### Hacer
- **Tomar nota del tiempo** cada vez que se menciona una actividad.
- **Preguntar por errores** ("¿alguna vez se derivó el lead equivocado?").
- **Preguntar por workarounds** ("¿usás algún Excel / planilla / app adicional?").
- **Pedir que abra la pantalla** si es remoto y se siente cómodo — ver es 10× mejor que escuchar.

### No hacer
- **No interrumpir los primeros 3 minutos.**
- **No sugerir soluciones** ("ah, eso se automatiza").
- **No juzgar prácticas ineficientes** — crea defensividad.
- **No pasar a la próxima tarea hasta cuantificar la actual.**

---

## Síntesis post-sesión

Al final de cada yesterday morning, producir:

```markdown
## Resumen Yesterday Morning — {{name}} — {{date}}

**Ventana narrada:** 8:30 - 12:00 AM del {{fecha del día anterior}}.

**Tareas identificadas:**
1. {{task}} — {{tiempo}} — {{sistema}}
2. ...

**Candidatos a IA:**
-

**Candidatos a automation:**
-

**Handoffs problemáticos:**
-

**Workarounds detectados:**
-

**Follow-ups:**
-
```

---

## Multiplicador: "Yesterday by role"

Entrevistar a 2 personas distintas en el mismo rol para comparar.

- Si hacen lo mismo con diferencia < 20% → proceso estándar, automatizable.
- Si hacen lo mismo con diferencia > 30% → proceso tribal, primero estandarizar, después automatizar.

Esta comparación descubre dónde la productividad varía por persona, no por proceso.

---

## Complemento: Shadowing

Cuando el empleado acepta, sentarse a su lado (o compartir pantalla) durante una hora **real** de trabajo. Regla:

- **No interrumpir.**
- **Tomar notas en pestaña propia.**
- **Marcar timestamps cada cambio de actividad.**

Shadowing de 1 hora a veces da más data que 3 entrevistas.

---

## Output al audit

Las tareas extraídas vía yesterday morning se vuelcan directamente a `/audit/task-map-template.md`. Las insights a `/audit/business-map-template.md`. Los candidatos a IA/automation al opportunity matrix inicial.

## Referencias

- `/audit/employee-interviews.md` — contexto general de entrevistas a operadores
- `/audit/task-map-template.md` — plantilla destino
- `/audit/roi-first-framework.md` — cómo encaja en el flujo
