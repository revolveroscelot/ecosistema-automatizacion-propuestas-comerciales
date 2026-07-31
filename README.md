# Ecosistema de Automatización IA — Generación de Propuestas Comerciales

Ecosistema de automatización que genera, valida y envía propuestas comerciales
personalizadas de extremo a extremo, con un punto de validación humana (HITL)
antes de contactar al cliente final.

## Caso de uso

Automatización del proceso de generación de propuestas comerciales: un cliente
solicita una propuesta, el sistema la redacta con IA a partir de datos
estructurados en Airtable, un humano la revisa y aprueba, y recién entonces
se envía por correo al cliente.

## Tecnologías integradas

| Componente | Herramienta |
|---|---|
| Orquestador | n8n (2 workflows) |
| Base de datos | Airtable |
| Procesamiento IA | Claude Sonnet 4.5 (vía OpenRouter) |
| Canal de salida | Gmail |

## Arquitectura

Ver diagrama y documentación completa en
[`Arquitectura_Ecosistema_Propuestas.pdf`](./Arquitectura_Ecosistema_Propuestas.pdf).

**Flujo A — Generación de propuesta:** Airtable Trigger (Status=Pendiente) →
validación de campos obligatorios → llamada a Claude vía OpenRouter → guardado
en Airtable → notificación al revisor humano (HITL). Incluye rutas de error
ante datos faltantes y ante fallos de la API de IA.

**Flujo B — Aprobación y envío:** Airtable Trigger (cambios de Status) → filtro
por "Aprobado por humano" → envío del correo final al cliente → actualización
de Status a "Enviado/Error".

## Estructura del repositorio

/
├── Arquitectura_Ecosistema_Propuestas.pdf
├── /workflows
│ ├── flujo_A_generacion_propuesta.json
│ └── flujo_B_aprobacion_envio.json
└── /evidencias
├── 01_caso_feliz.png
├── 02_dato_faltante.png
├── 03_fallo_api.png
├── 04_repeticion_caso_feliz.png
└── 05_flujo_completo_aprobacion.png

## Enlaces

- **Base de datos (solo lectura): https://airtable.com/appk7F3Ogd0HaVpx8/shrUVJIeISVf5SsL0
- **Video demo (3 min):** https://drive.google.com/file/d/128c5UR5tr-8ocg5H5BVa5iteksjYpHBw/view?usp=sharing
- **Dashboard de control (KPIs y tasa de errores): https://airtable.com/appk7F3Ogd0HaVpx8/shrUVJIeISVf5SsL0
