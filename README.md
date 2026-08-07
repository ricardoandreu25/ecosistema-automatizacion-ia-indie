# Ecosistema de Automatización IA para la Gestión de Contenidos de Indie

Proyecto desarrollado como entrega final del curso de **Arquitecturas de Automatización con Inteligencia Artificial**.

El sistema automatiza de extremo a extremo el proceso de generación, revisión y aprobación de contenidos para redes sociales mediante la integración de **Make**, **Airtable**, **OpenAI** y **Slack**, incorporando un flujo de **Human-in-the-Loop (HITL)** y mecanismos de resiliencia mediante **Error Handlers**.

---

# Tecnologías utilizadas

- **Orquestador:** Make
- **Base de datos:** Airtable
- **Procesamiento IA:** OpenAI (GPT-5.6-terra)
- **Canal de salida:** Slack

---

# Arquitectura del sistema

El proyecto se compone de dos escenarios principales.

## Escenario 1 – Generación automática de contenidos

1. Airtable detecta una nueva idea de contenido.
2. Se consulta la base de conocimiento almacenada en Airtable.
3. El módulo **Text Aggregator** reúne toda la información recuperada en un único bloque de contexto.
4. OpenAI genera automáticamente el borrador del contenido.
5. Airtable actualiza el registro con el borrador generado y cambia el estado a **En revisión**.
6. Slack envía una notificación para que el contenido sea revisado por una persona.
7. Si ocurre un error durante la llamada a OpenAI, un **Error Handler** registra la incidencia en Airtable y finaliza la ejecución mediante un módulo **Resume**, evitando la interrupción completa del escenario.

---

## Escenario 2 – Revisión editorial (Human-in-the-Loop)

El segundo escenario comienza cuando un revisor actualiza el registro en Airtable.

Un **Router** divide el flujo en dos rutas:

### Ruta de aprobación

- El contenido cambia al estado **Publicado**.
- Airtable actualiza el registro.
- Slack envía una notificación informando que el contenido fue aprobado.

### Ruta de rechazo

- OpenAI genera automáticamente una nueva versión utilizando los comentarios del revisor.
- Airtable reemplaza el borrador anterior por la nueva propuesta.
- Slack informa que se generó una nueva versión para revisión.

---

# Human-in-the-Loop (HITL)

Antes de cualquier publicación existe una validación humana obligatoria.

El revisor analiza el contenido generado por la IA y decide si:

- aprobar el contenido para su publicación;
- rechazarlo indicando comentarios para generar una nueva versión.

Este mecanismo evita publicaciones automáticas sin supervisión humana.

---

# Gestión de errores

El Escenario 1 incorpora un **Error Handler** asociado al módulo **OpenAI – Generate a response**.

Ante un fallo durante la llamada a la API:

- se registra la incidencia en Airtable;
- el estado del contenido pasa a **Error**;
- se conserva la trazabilidad del proceso;
- el escenario continúa mediante un módulo **Resume**, evitando detener futuras ejecuciones del flujo.

---

# Optimización implementada

Para optimizar el consumo de la API de OpenAI se incorporó un **Text Aggregator**, que consolida toda la información recuperada desde la base de conocimiento antes de enviarla al modelo.

Esta estrategia permite:

- reducir la cantidad de llamadas a OpenAI;
- disminuir el consumo de créditos;
- proporcionar un contexto más completo para la generación del contenido.

---

# Contenido del repositorio

```
├── blueprints.
    ├── Escenario_1_Generacion_Automatica_Contenidos.blueprint.json
    ├── Escenario_1_Generacion_Automatica_Contenidos.blueprint.json
├── documentacion
    ├── Trabajo_Final_AI_AUTOMATION.pdf
├── screenshots
│   ├── figura1-arquitectura-general.png
│   ├── figura2-escenario1-generacion.png
│   ├── figura3-ruta-aprobados.png
│   ├── figura4-ruta-rechazados.png
│   ├── figura5-airtable-contenidos.png
│   └── figura6-dashboard-control.png
├── README.md
└── Video_Demo.mp4
```

---

# Funcionalidades implementadas

- Generación automática de contenidos mediante IA.
- Base de conocimiento administrada en Airtable.
- Recuperación de contexto mediante Search Records.
- Consolidación del contexto utilizando Text Aggregator.
- Generación automática de borradores con OpenAI.
- Actualización automática de estados en Airtable.
- Notificaciones automáticas mediante Slack.
- Validación humana (Human-in-the-Loop).
- Regeneración automática de contenidos rechazados.
- Gestión de errores mediante Error Handler y Resume.
- Dashboard de control en Airtable para el seguimiento del pipeline.

---

# Video Demo

**Archivo:**

- `Video_Demo.mp4`

---

## Enlaces

- Enlace al Dashboard de Control: https://airtable.com/app8hXFVxZISymAOA/shro8Zj1WsWr8X7oQ/tblW8vd484GxBLazF
- Base de datos (Airtable - modo lectura): https://airtable.com/...](https://airtable.com/invite/l?inviteId=invVqFGXy1BYSKVtG&inviteToken=9538f9c95da436b79715cd9379b3a96cd969920acd30d026c157063f70ca3abb&utm_medium=email&utm_source=product_team&utm_content=transactional-alerts

---

# Autor

**Ricardo Faustino Andreu Monteserin**

Entrega Final – Arquitecturas de Automatización con Inteligencia Artificial.
