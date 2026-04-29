# Change Management — Gestión del cambio humano

Implementar IA sin gestionar el cambio humano es la causa #1 de fracaso. Este documento describe cómo JM lo gestiona **antes, durante y después** del rollout.

## Filosofía

> La herramienta no transforma si la persona no la adopta. Y la persona no adopta si siente amenaza, si no entiende, o si no recibe apoyo.

## Los 3 miedos universales

1. **"Me van a despedir."** → Respuesta: el audit muestra cómo liberarse de lo aburrido para hacer lo interesante.
2. **"No voy a saber usarlo."** → Respuesta: training + FAQ + canal de soporte + iteración.
3. **"Va a hacerlo mal y el culpable voy a ser yo."** → Respuesta: el humano queda en el loop, la IA propone y el humano aprueba (al menos inicialmente).

Todo plan de change management responde a estos tres miedos explícitamente.

---

## Fases del change management

### Fase 0 — Pre-implementación (durante el audit)

Antes de escribir una línea de código, comunicar:

1. **Kickoff con el equipo afectado** (no solo sponsor). 30 min.
   - "Por qué estamos haciendo esto."
   - "Qué NO estamos haciendo."
   - "Qué va a cambiar en tu día a día."
   - Preguntas abiertas, nadie toma lista.

2. **Compromiso explícito del sponsor.**
   - "Nadie pierde el trabajo por esto. Nuestro compromiso es que el tiempo liberado se use para X."
   - Por escrito, firmado por el sponsor, compartido al equipo.

3. **Identificar champions.**
   - 1-2 personas por equipo que son "adoptadores tempranos".
   - Son los testers iniciales y los ambassadors del cambio.
   - Incentivo: reconocimiento + participación en diseño.

### Fase 1 — Durante la implementación (sprint)

4. **Demo semanal al equipo.** 15 min.
   - Mostrar lo que se construyó esa semana.
   - Escuchar reacciones crudas.
   - Ajustar.

5. **Documentación progresiva.**
   - FAQ actualizado semanalmente con lo que los champions preguntan.
   - Manual final listo 1 semana antes del rollout (no el día).

6. **Sesiones de hands-on.**
   - Champions usan el sistema en sandbox.
   - Se graban errores y confusión para mejorar UX.

### Fase 2 — Rollout (canary → 100%)

7. **Training formal.**
   - 1 sesión de 1 hora, grabada.
   - Formato: 50% demo, 30% hands-on, 20% Q&A.
   - Cada usuario final pasa por el training antes de que le llegue la herramienta.

8. **Office hours diarios.**
   - Durante las primeras 2 semanas post 100%, 30 min/día de soporte abierto.
   - Un JM presente en Slack / call.

9. **Canal de feedback continuo.**
   - Slack channel o formulario corto.
   - Regla: toda sugerencia recibe respuesta en < 48 h (aunque sea "no haremos esto").

### Fase 3 — Post-rollout (mantenimiento)

10. **Revisión mensual con equipo afectado.** 30 min.
    - ¿Qué funciona?
    - ¿Qué no?
    - ¿Qué te gustaría que cambiara?

11. **Tracking de adopción.**
    - % del equipo usando la herramienta semanalmente.
    - % de tareas procesadas vs teóricamente procesables.
    - NPS del operador.

12. **Reconocimiento.**
    - Compartir casos de uso exitosos internamente (con permiso).
    - Mostrar horas liberadas / trabajo nuevo hecho gracias al tiempo ahorrado.

---

## Mensaje inicial al equipo — template

```
[Enviar 2 semanas antes del kickoff del sprint]

Equipo,

Durante las próximas {{N}} semanas, vamos a trabajar con JM Consulting en
implementar {{descripción corta}} en el área de {{área}}.

Lo que quiero que sepan:

1. Nadie pierde el trabajo por esto.
   Nuestro objetivo es liberar tiempo suyo de tareas que honestamente no
   son la razón por la que los contratamos, para que puedan hacer más de
   lo que sí importa: {{tareas valiosas de su rol}}.

2. No les vamos a tirar una herramienta de un día para otro.
   Van a ser parte del diseño. {{Champion 1}} y {{Champion 2}} van a ser
   los primeros en probar y darán feedback directo a JM.

3. Si algo no funciona, lo cambiamos.
   Si sienten que el sistema les complica la vida, la regla es decirlo.
   Literalmente ningún cambio entra en producción si las personas del
   equipo no lo avalan.

4. Training formal llegará en {{N}} semanas.
   Sesión de 1 hora, grabada. Todos quienes usen la herramienta pasan por
   eso. No hay examen, no hay evaluación.

Cualquier duda me la mandan directo a mí, no hay filtro.

{{Nombre sponsor}}
```

Este mensaje lo escribe el sponsor, no JM. JM solo lo redacta y el sponsor firma.

---

## Lo que NO se hace

- **No decir "esto mejora la productividad" sin explicar qué pasa con las horas liberadas.**
- **No mostrar comparaciones entre personas** ("María procesó 30% más que Juan").
- **No implementar nada a escondidas** bajo el argumento de "no queremos generar ansiedad".
- **No tercerizar el comunicado** a JM. El sponsor es el que habla.
- **No prometer "no va a haber cambios"** — habrá. Prometer que los cambios son conversados.

---

## Cuando alguien se resiste

Señales:
- No viene a las demos.
- No participa en sesiones de feedback.
- Hace comentarios tóxicos en los pasillos.
- Usa la herramienta mal deliberadamente para demostrar que no sirve.

Respuesta:
1. **1:1 del sponsor con la persona, no del consultor.** El miedo es interno, no con JM.
2. **Escuchar primero.** La resistencia casi siempre es miedo no expresado.
3. **Validar el miedo.** "Tiene sentido que te preocupe X."
4. **Mostrar compromiso concreto.** "Si al cabo de 3 meses esto no funciona para vos, lo revisamos."
5. **Involucrar.** Pedirle explícitamente que sea revisor de algo.

Si después de 6-8 semanas la resistencia activa persiste y el sponsor identifica un problema serio, el sponsor gestiona (no JM). JM no participa en conversaciones de performance.

---

## Métricas del change management

Tracking mensual (post rollout):

| Métrica | Target | Fuente |
|---|---|---|
| % equipo usando la herramienta/sem | > 80% al mes 3 | Logs |
| NPS operador | > 30 al mes 3 | Encuesta |
| Tickets de soporte JM | < 5/mes al mes 3 | Slack/email log |
| Sugerencias recibidas | > 3/mes | Canal feedback |
| Sugerencias implementadas | > 30% | Iteraciones |
| Rotación del equipo afectado | ≤ rotación empresa | HR |

Si el tercer mes no llegamos al 80% de uso, el change management falló y JM lleva parte de la responsabilidad.

---

## Entregables del change management

- [ ] Mensaje inicial del sponsor (2 semanas antes).
- [ ] Identificación de champions (1 semana antes).
- [ ] Demos semanales durante el sprint (4 demos).
- [ ] Training de 1 h grabado (antes de canary).
- [ ] Manual del usuario + FAQ (antes de canary).
- [ ] Office hours diarios durante 2 semanas post 100%.
- [ ] Canal de feedback activo.
- [ ] Revisión mensual durante los primeros 3 meses.
- [ ] Reporte de métricas de adopción mensual.

---

## Ver también

- `/delivery/rollout-plan.md` — contexto del rollout técnico
- `/delivery/quick-wins-sprint.md` — estructura del sprint
- `/maintenance/monthly-review-template.md` — seguimiento post-proyecto
