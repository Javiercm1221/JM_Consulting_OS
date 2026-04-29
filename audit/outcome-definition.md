# Outcome Definition — Paso 1 del audit

Plantilla para definir los outcomes del sponsor ejecutivo. **Sin esto firmado no hay audit.**

## Objetivo

Traducir deseos difusos ("queremos IA") en resultados económicos medibles y atribuibles.

## Entregable

Un documento de 1 página con 3-5 outcomes, aprobado por el sponsor (firma digital o email confirmando).

---

## Estructura del documento

### Encabezado
```
Cliente: {{company}}
Sponsor: {{name}} — {{role}}
Fecha: {{YYYY-MM-DD}}
Audit: AI Opportunity Audit · Versión 1.0
Duración del audit: 10 días hábiles
Rango de outcomes: 12 meses
```

### Outcomes (3-5)

Para cada outcome:

```
Outcome #1: {{nombre descriptivo}}

Descripción: {{1 frase}}
Métrica primaria: {{nombre exacto}}
Baseline actual: {{número + fecha de medición}}
Target a 12 meses: {{número}}
Sponsor del outcome: {{quién rinde cuentas del número}}
Dependencias externas: {{cosas fuera de control}}
Definición de "éxito": {{frase concreta}}
Definición de "fracaso": {{frase concreta}}
```

### Outcomes de ejemplo (usar como referencia)

**Ejemplo 1 — Growth sin headcount**
```
Métrica: ARR por FTE
Baseline: 120K USD/FTE
Target 12m: 180K USD/FTE
Sponsor: CEO
Éxito: 50% crecimiento con <10% más headcount
Fracaso: crecimiento de ARR con >20% más cabezas
```

**Ejemplo 2 — Lead response**
```
Métrica: Time-to-first-touch (leads web)
Baseline: 3.2 h promedio
Target 12m: < 5 min (95 percentil)
Sponsor: VP Sales
Éxito: conversión lead→tour sube ≥ 3 puntos
Fracaso: menos del 50% de leads con respuesta < 5 min
```

**Ejemplo 3 — Costo back-office**
```
Métrica: Horas admin / unidad gestionada
Baseline: 2.1 h/mes
Target 12m: 1.0 h/mes
Sponsor: COO
Éxito: mantener calidad (SLA 95%) con 50% menos horas
Fracaso: bajar horas pero con tickets +20% o SLA cae
```

---

## Preguntas para la sesión de outcomes

### Apertura (5 min)
1. ¿Cuál es la foto de {{company}} a 12 meses que querés ver?
2. ¿Qué cosa te haría decir "este año fue el mejor de la década"?

### Fugas conocidas (10 min)
3. ¿Dónde sabés que se te escapa plata y todavía no lo arreglaste?
4. ¿Por qué no lo arreglaste?
5. Si me dieras una lista mental de "cosas que deberíamos automatizar", ¿qué diría?

### Crecimiento (10 min)
6. ¿Qué métrica de negocio tiene que subir?
7. ¿Qué tiene que bajar?
8. ¿Hay alguna métrica donde una mejora de 10% cambia la conversación a 3 años?

### Restricciones (5 min)
9. ¿Qué no podés tocar? (equipos protegidos, clientes sensibles, regulación)
10. ¿Hay líneas rojas de compliance / privacidad?
11. ¿Cuánto podrías invertir en 2026 en automatización sin pedir board approval?

### Alineación (5 min)
12. ¿Quién más tiene que estar de acuerdo con estos outcomes?
13. ¿A quién vamos a entrevistar para mapear?

---

## Criterios de calidad del outcome

Un outcome se considera válido si cumple **los 5 criterios**:

1. **Medible:** se puede poner un número hoy y dentro de 12 meses.
2. **Atribuible:** se puede rastrear al trabajo del audit / implementación.
3. **Material:** mover el número genera al menos 100K USD de valor.
4. **Accionable:** hay tareas humanas identificables detrás del número.
5. **Aprobado:** el sponsor lo firma.

**Si un outcome no cumple los 5, reescribir o descartar antes de avanzar.**

---

## Output final — formato

Archivo: `/delivery/clients/{{company}}/outcomes-{{YYYY-MM-DD}}.md`

Estructura:
```markdown
# Outcomes — {{company}}
Fecha: {{date}}
Sponsor: {{name}}

## Resumen ejecutivo
- 3-5 outcomes priorizados
- Valor estimado combinado: USD {{total}}/año
- Audit budget: USD 10K

## Outcomes

### 1. {{nombre}}
...

### 2. {{nombre}}
...

## Exclusiones
- {{cosa que NO está en scope}}

## Firma
Sponsor: __________________ Fecha: __________________
Consultant: Javier Mendoza — JM Consulting
```

---

## Anti-patterns (qué NO aceptar)

- "Queremos IA en toda la empresa." → Reframe: "¿Qué métrica cambia?"
- "Mejorar eficiencia." → Reframe: "¿Qué tarea se hace más rápido y cuánto vale?"
- "Estar al día con la tecnología." → Reframe: "¿Qué competidor te está comiendo y con qué?"
- Outcomes sin dueño. → No hay accountability = no hay outcome.
- Outcomes a 3 años. → Fuera de scope del audit. Máximo 12 meses.

---

## Referencias

- Paso siguiente: `/audit/stakeholder-interviews.md`
- Framework completo: `/audit/roi-first-framework.md`
