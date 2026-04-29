# Billing SOPs — COO

## SOP mensual de facturación

| Día del mes | Acción |
|---|---|
| Día 1 | Generar facturas de retainers activos |
| Día 2 | Generar facturas de milestones cerrados el mes anterior |
| Día 3 | Enviar facturas a clientes vía email + link de pago (Stripe) |
| Día 15 | Recordatorio a facturas no pagas |
| Día 25 | Escalar a cliente + CEO si > 25 días sin pago |
| Día 31 | Email formal si sigue sin pago |
| Día 45 | Pausa de servicios no críticos (con aviso escrito) |
| Día 60 | Escalation a Javier + legal si corresponde |

## Template recordatorio de pago (Día 15)

```
Asunto: Recordatorio — Factura #[número] vence [fecha]

Hola [nombre],

Le recordamos que la factura #[número] por $[monto] 
por [descripción del servicio] vence el [fecha].

Link de pago: [Stripe link]

Si ya realizó el pago, ignore este mensaje.
Ante cualquier consulta, respondemos este email.

Clara · JM Consulting
```

## SOP retainer renewal

30 días antes del vencimiento:
1. Chequear consumo del cliente (horas usadas vs. tier contratado).
2. Preparar propuesta de renovación: mismo tier / upgrade / downgrade.
3. Enviar a Client Success para entrega al cliente.
4. Si downgrade: escalar al CRO y CEO antes de enviar.

## SOP nuevo cliente onboarding (trigger: CRO confirma firma SOW)

1. Crear cliente en CRM (HubSpot) con todos los datos.
2. Crear factura inicial en Stripe (pago del audit o primer milestone).
3. Crear carpeta del cliente en Google Drive (`_active/<client-slug>/`).
4. Crear canal de Slack `#cli-[slug]` e invitar a agentes asignados.
5. Enviar welcome email con next steps y acceso al Calendly de Javier.
6. Confirmar que kickoff está agendado.
7. Notificar al CEO que el cliente está en sistema.

## SOP weekly close (Viernes 17:00 ET)

1. Pull de data de todas las herramientas (Stripe, HubSpot, Slack).
2. Revisar facturas pendientes vs. pagadas.
3. Revisar P&L de la semana (revenue reconocido vs. costos incurridos).
4. Generar report semanal al CEO.
5. Backup de datos críticos (export de CRM, Stripe report).
