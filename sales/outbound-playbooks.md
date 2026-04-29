# Outbound Playbooks

Playbook operativo completo del growth engine. Cada canal tiene su propio flujo, SOP y métricas.

## Canales de adquisición

Por orden de prioridad:

1. Red propia (referrals).
2. Email outbound.
3. LinkedIn outbound.
4. Cold calling (para nichos locales).
5. YouTube / contenido (long-term).
6. Ads (cuando hay case studies).

## Flujo operativo completo (aplicable a cualquier canal)

```
1. Elegir nicho o mercado
2. Hacer scraping de empresas
3. Enriquecer contactos
4. Filtrar comercialmente
5. Armar base de leads
6. Redactar outreach
7. Cargar campaña
8. Hacer follow-up
9. Conseguir reuniones
```

## Playbook 1 — Email outbound (principal)

### Stack
- **Scraping/Enrichment:** Apify + Apollo + Clay + Vibe Prospecting.
- **Verificación:** NeverBounce o similar.
- **Envío:** Instantly.ai (múltiples inboxes warmed up).
- **Tracking:** Instantly + Sheets/Airtable + CRM.

### Infraestructura mínima
- 3-5 dominios secundarios (nunca mandar desde el principal).
- 2 inboxes por dominio.
- 3-4 semanas de warmup antes de enviar.
- SPF / DKIM / DMARC configurados.
- Volumen: 25-40 emails/inbox/día máximo al inicio.

### Secuencia estándar (4 toques)

| Día | Toque | Objetivo |
|---|---|---|
| 0 | Email 1 — gancho + dolor | Generar curiosidad |
| 3 | Email 2 — caso de uso + prueba social | Credibilidad |
| 7 | Email 3 — oferta clara (audit) | CTA |
| 14 | Email 4 — break-up | Reactivar |

### Métricas target
- Open rate > 50%.
- Reply rate > 3%.
- Positive reply rate > 1.5%.
- Meetings booked / 100 leads > 1.

### SOP rápido
1. Exportar lista verificada.
2. Cargar en Instantly.
3. Asignar inboxes.
4. Lanzar secuencia.
5. Responder a positivos en < 60 min (hot leads).
6. Mover a CRM (stage: discovery requested).

## Playbook 2 — LinkedIn outbound

### Stack
- Sales Navigator.
- HeyReach o Expandi para automation.
- LinkedIn native para touchpoints manuales.

### Secuencia estándar
1. Day 0 — Connection request con contexto (sin pitch).
2. Day 2 — Mensaje de valor (insight/recurso).
3. Day 7 — Mensaje con dolor + pregunta abierta.
4. Day 14 — CTA a discovery call.
5. Day 21 — Break-up.

### Métricas target
- Connection acceptance > 30%.
- Reply rate > 10% (sobre aceptados).
- Meetings / 100 accepted > 3.

## Playbook 3 — Cold calling (nicho local)

### Cuándo usarlo
- Servicios locales (HVAC, roofing, clínicas, dentistas).
- Decisor es el dueño o un gerente accesible.
- Ticket bajo-medio con ciclo de decisión rápido.

### SOP
1. Lista de 50-100 empresas del nicho + ciudad.
2. Investigar 3 min por empresa.
3. Llamar, pedir al decisor por nombre.
4. 10 segundos de pitch → pregunta dolor → CTA reunión.
5. Follow-up por email en < 1 hora.

### Métricas target
- Contacto con decisor > 15%.
- Reunión agendada / contacto efectivo > 10%.

## Playbook 4 — Referidos

### Flujo
1. Después de cada proyecto cerrado, preguntar explícitamente.
2. Template de intro facilitado al cliente.
3. Incentivo: 10% del primer proyecto (o mes gratis de retainer) al referidor.
4. Tracking en CRM.

## Playbook 5 — Contenido (LinkedIn + YouTube)

### Frecuencia
- LinkedIn: 3 posts/semana.
- Newsletter: 1 / semana.
- YouTube: 2 videos / mes.

### Temas pilar
- Casos reales de ROI.
- Desmitificación de IA en vertical.
- Behind the scenes del delivery.
- Frameworks propios (yesterday morning, opportunity matrix, ROI model).

## Propuesta de valor por canal (para copy)

- Más reuniones.
- Más velocidad comercial.
- Menos trabajo manual.
- Mejor seguimiento.
- Menos tiempo investigando prospectos.

## Reglas de oro

- **No vender scraping. Vender infraestructura comercial.**
- **Arrancar con ofertas fáciles de entender:** te genero reuniones · te consigo leads · te hago outreach · te armo campañas · te detecto negocios sin web.
- **Personalizar siempre el gancho inicial.** Los cuerpos pueden ser templates, la primera línea no.
- **Responder positivos en < 60 min.**
- **Nunca hablar del producto antes de entender el dolor.**

## SOPs técnicos referenciados

- `/sales/sop-apify.md`
- `/sales/sop-vibe-prospecting.md`
- `/sales/sop-apollo.md`
- `/sales/sop-instantly.md`
- `/sales/sop-clay.md`
- `/sales/sop-heyreach.md`
- `/sales/sop-browser-based-execution.md`

Estos SOPs se construyen on-the-fly cuando se ejecuta cada canal, documentando el flujo real usado en el mes 1 de operación.
