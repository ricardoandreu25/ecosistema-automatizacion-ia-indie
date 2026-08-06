# Ecosistema de Automatización IA para Pipeline de Contenidos

## Descripción

Proyecto final desarrollado para el curso Arquitectura de Automatización Inteligente de Coderhouse.

El proyecto implementa un ecosistema de automatización para la generación, revisión y aprobación de contenidos digitales de Indie Punta del Este. La solución integra Make, Airtable, OpenAI y Slack para gestionar el ciclo completo de un contenido, desde el ingreso de una idea hasta su aprobación, rechazo o corrección.

## Funcionalidades principales

- Generación automática de borradores mediante OpenAI.
- Recuperación de contexto desde una base de conocimiento en Airtable.
- Revisión editorial con Human in the Loop.
- Rutas diferenciadas para contenidos aprobados y rechazados.
- Regeneración automática según comentarios del revisor.
- Manejo de errores mediante Error Handler y Resume.
- Registro de estados y trazabilidad en Airtable.
- Dashboard de control para el seguimiento del pipeline.

## Tecnologías utilizadas

- Make
- Airtable
- OpenAI
- Slack
- GitHub

## Arquitectura

![Arquitectura general](01_arquitectura_general.png)

## Estructura del repositorio

- `blueprints/`: archivos exportados de los escenarios de Make.
- `screenshots/`: capturas de arquitectura, escenarios, Airtable y dashboard.
- `documentacion/`: documento técnico final en formato PDF.

## Escenarios

### Escenario 1 – Generación automática de contenidos

Detecta ideas con estado `Generando`, recupera contexto desde Airtable, genera un borrador con OpenAI, actualiza el registro a `En revisión` y envía una notificación mediante Slack.

### Escenario 2 – Revisión editorial y Human in the Loop

Procesa la decisión del revisor. Si el contenido es aprobado, actualiza el registro y notifica el resultado. Si es rechazado, utiliza los comentarios editoriales para generar una nueva versión mediante OpenAI.

## Dashboard de control

El dashboard permite visualizar el estado de los contenidos, las aprobaciones, los rechazos y los errores registrados durante la ejecución del sistema.

**Enlace al dashboard:**

(https://airtable.com/app8hXFVxZISymAOA/shro8Zj1WsWr8X7oQ/tblW8vd484GxBLazF)

## Documentación

El documento técnico completo se encuentra en:

`documentacion/Trabajo_Final_IA_Automation.pdf`

## Autor

Ricardo Faustino Andreu Monteserin

Trabajo Final – Arquitectura de Automatización Inteligente  
Coderhouse
