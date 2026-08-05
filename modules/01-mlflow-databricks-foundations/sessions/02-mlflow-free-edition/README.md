# Sesión 02 — Tracking, trazas y evaluación en Free Edition

**Duración:** 1 hora de demostración/concepto + 1 hora de práctica

## Resultado de aprendizaje

El alumnado crea dos *runs* comparables en el experimento de su propio notebook
de Databricks Free Edition, inspecciona una traza de agente y ejecuta una
evaluación de LLMOps sin depender de un endpoint de pago.

## Secuencia

### Concepto breve (15 min)

Explica por qué Free Edition usa experimentos de notebook: el compute es
serverless y limitado, y cada estudiante puede reproducir su evidencia sin
permisos sobre un experimento compartido. Distingue métrica de modelo, traza de
aplicación y *scorer* de evaluación.

### Construcción en directo (45 min)

Ejecuta primero
[`01_tracking_mlop_solucion.ipynb`](../../notebooks/01_tracking_mlop_solucion.ipynb)
y muestra los parámetros, artefactos de riesgos, F1, recall y ROC AUC. Después
ejecuta el modo determinista de
[`02_agent_llmops_solucion.ipynb`](../../notebooks/02_agent_llmops_solucion.ipynb)
y abre la traza resultante.

### Extensión independiente (45 min)

El alumnado completa las versiones sin resolver
[`01_tracking_mlop.ipynb`](../../notebooks/01_tracking_mlop.ipynb) y
[`02_agent_llmops.ipynb`](../../notebooks/02_agent_llmops.ipynb), siguiendo la
[práctica de semana 01](../../exercises/01_project_risks_and_tracking.md).

### Debrief (15 min)

Compara una tabla de dos *runs* y una evaluación. Cierra con dos preguntas:
qué evidencia falta antes de producción y qué limitación del *scorer* requiere
una capa adicional de evaluación.
