# Employee Interviews — Entrevistas a operadores

Plantilla para entrevistar a **quienes hacen el trabajo todos los días**. Aquí está el oro del audit.

## Por qué importa

Los ejecutivos saben **qué** quieren, pero no **cómo** se hace.
Los operadores saben **cómo** se hace de verdad — incluyendo los hacks, los workarounds y los re-trabajos invisibles.

> Si solo entrevistás a C-level, tu audit es teórico. Si entrevistás a operadores, tu audit es accionable.

## Duración

30 minutos por operador.

## Cuántos

Mínimo 5 operadores por audit. Preferible 2 por proceso crítico.

## Perfil a entrevistar

- Quien responde primero un lead.
- Quien hace reconciliación / data entry.
- Quien atiende tickets de soporte.
- Quien arma documentos repetitivos.
- Quien coordina handoffs entre áreas.
- Quien maneja herramientas de datos (dashboards, ETL).

---

## Apertura (3 min)

```
"Gracias por el tiempo. Tu jefe/managing partner me pidió que mapeara
cómo se hacen las cosas en {{área}} para ver qué se puede hacer más fácil.

Esto NO es una evaluación de vos. Al revés: si encontramos formas de
automatizar tareas aburridas, vos vas a hacer más de lo interesante.

Lo que más me sirve es que me cuentes lo que hiciste ayer en detalle,
paso a paso, como si fuera nuevo. ¿Te parece?"
```

Importante: bajar ansiedad. **Si el empleado cree que viene una ola de despidos, oculta información.**

---

## Bloque 1 — Yesterday morning (15 min)

```
"Contame tu mañana de ayer paso a paso. ¿Qué fue lo primero que hiciste?"
```

Seguir con:
- "¿Y después?"
- "¿Cuánto tardaste?"
- "¿De dónde sacaste ese dato?"
- "¿A dónde lo mandaste?"
- "¿Cómo sabías que estaba listo?"
- "¿Qué pasó si había error?"

Objetivo: reconstruir 2-3 horas reales con cronometraje minuto a minuto.

Ver `/audit/yesterday-morning-method.md` para detalle.

---

## Bloque 2 — Tareas recurrentes (10 min)

1. ¿Qué tarea te toma más tiempo en la semana? ¿Cuánto?
2. ¿Cuál te parece más aburrida / repetitiva?
3. ¿Cuál te gustaría dejar de hacer si pudieras?
4. ¿Cuál es la que más errores genera?
5. ¿Cuál dependés de otro para empezar? ¿Cuánto esperás?
6. ¿Qué hacés cuando el sistema X no responde?
7. ¿Qué atajos armaste (excels, scripts, plantillas) para sobrevivir?

---

## Bloque 3 — Herramientas (5 min)

8. ¿Qué software usás en el día?
9. ¿Cuál te frustra más?
10. ¿Cuál te gusta?
11. ¿Qué información tenés que buscar en 2+ sistemas?
12. ¿Hay alguna tarea que hacés en Excel porque ningún sistema la soporta?

---

## Bloque 4 — Ideas del operador (5 min)

13. Si pudieras cambiar una cosa de tu día a día, ¿cuál sería?
14. ¿Qué te gustaría aprender a usar que hoy no usás?
15. ¿Viste algún software o demo que te pareció que te podría ayudar?
16. ¿Hay alguna tarea donde pensás "esto lo tendría que hacer una máquina"?

---

## Bloque 5 — Cierre (2 min)

17. ¿Hay algo que no te pregunté y pensás que me serviría saber?
18. ¿A qué otro compañero me recomendás hablar?

```
"Gracias. Si tenés algo más que recordás después, mandame un mensaje."
```

---

## Plantilla de notas

```markdown
# Entrevista: {{name}} ({{role}}) — {{área}}
Fecha: {{date}}
Duración: {{min}}

## Tareas mapeadas (agregar a task map)

| Task | Frec | Tiempo/vez | Sistemas | Handoff a |
|---|---|---|---|---|
| | | | | |

## Dolor top 3
1.
2.
3.

## Workarounds / hacks encontrados
-

## Oportunidades evidentes
-

## Sentimiento del operador
- Abierto al cambio / neutral / resistente
- Razón:

## Quotes
> "..."
```

---

## Señales a registrar

### Señales de fuga económica
- "Siempre espero a que X me mande..." → handoff lento.
- "Cada vez que hago esto reviso 3 veces porque si me equivoco..." → re-trabajo por miedo.
- "En Excel tengo una planilla que..." → proceso no capturado por sistemas.
- "Cuando viene el mes cerrado me quedo hasta las 10..." → overflow estacional.
- "Le pregunto a Juan porque nunca entendí bien el sistema..." → conocimiento tribal.

### Señales de oportunidad IA clara
- Tarea repetitiva con input estructurado → clasificación / extracción.
- Tarea de redacción (emails, contratos, respuestas) → generación.
- Búsqueda de información en docs → RAG.
- Decisión de enrutamiento → clasificación.
- Consolidación de dashboards → automation.

### Señales de oportunidad de automation simple (no IA)
- Copy-paste entre sistemas → Zapier/n8n.
- Planillas Excel compartidas → base de datos.
- Emails manuales de status → webhooks.
- Reportes armados a mano → query + schedule.

---

## Reglas

- **Nunca compartir transcripts con management** sin permiso explícito.
- **Anonimizar ideas sensibles** en el deck final.
- **No corregir al operador** si dice algo impreciso técnicamente — su percepción es el dato.
- **Agradecer con nombre propio** en el deck ("Esta oportunidad salió de entrevistas con Juan y María").

---

## Post-entrevista

- [ ] Notas pasadas en limpio en < 24 h.
- [ ] Tareas nuevas agregadas al task map.
- [ ] Quotes útiles marcadas para el deck.
- [ ] Si surgieron ideas de quick wins evidentes, agregar al opportunity matrix como "candidata de entrevista".
- [ ] Follow-up agendado si quedó algo pendiente.

---

## Referencias

- `/audit/yesterday-morning-method.md` — detalle de la técnica
- `/audit/task-map-template.md` — dónde cargar tareas
- `/audit/business-map-template.md` — dónde encajar handoffs
