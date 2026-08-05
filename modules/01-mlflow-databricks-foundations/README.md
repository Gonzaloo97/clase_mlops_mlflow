# Semana 01 — De un notebook a una operación observable

## Resultado de aprendizaje

Al terminar la semana, el alumnado distingue un prototipo de un sistema
operable y puede registrar en Databricks un experimento de ML, una traza de
agente y una evaluación mínima de una aplicación con LLM. Sabe también qué
evidencias, riesgos y secretos no debe dejar fuera del ciclo de vida.

## Secuencia didáctica

El detalle por sesión está en [Sesión 01](sessions/01-prototipo-a-operacion/README.md)
y [Sesión 02](sessions/02-mlflow-free-edition/README.md).

### 1. Concepto breve — Clase 1 (120 min)

- Prototipo frente a producción: qué cambia cuando hay usuarios, costes,
  fallos, datos sensibles y requisitos de reproducibilidad.
- Un experimento como unidad común de evidencia: *runs* de entrenamiento,
  trazas de aplicaciones y evaluaciones de GenAI.
- Riesgos iniciales: datos, sesgo, seguridad, coste, latencia, alucinación y
  ausencia de trazabilidad.
- Lectura guiada de un notebook heredado: localizar valores codificados,
  rutas personales, artefactos frágiles y ausencia de un contrato de entrada.

### 2. Construcción en directo — Clase 2, primera hora (60 min)

El docente ejecuta las celdas esenciales de
[`notebooks/01_tracking_mlop_solucion.ipynb`](notebooks/01_tracking_mlop_solucion.ipynb): usa el
experimento propio del notebook, crea un *run* reproducible, registra métricas
y convierte el registro de riesgos en un artefacto. En la interfaz de MLflow se
comparan dos *runs* antes de discutir cuál es apto para avanzar.

### 3. Extensión independiente — Clase 2, segunda hora (60 min)

El alumnado sigue la [práctica](exercises/01_project_risks_and_tracking.md).
Primero modifica una decisión del modelo y justifica el resultado con datos de
MLflow. Después ejecuta el modo determinista de
[`notebooks/02_agent_llmops_solucion.ipynb`](notebooks/02_agent_llmops_solucion.ipynb), inspecciona la
traza y ejecuta el *scorer* de código. Si la cuenta tiene capacidad y el docente
lo indica, habilita la llamada a un endpoint como extensión; nunca con una clave
pegada en el notebook.

### 4. Debrief (20 min)

- ¿Qué evidencia permite reproducir o descartar un experimento?
- ¿Qué parte de la traza explica una respuesta incorrecta?
- ¿Qué métrica o *scorer* sería insuficiente para autorizar producción?
- ¿Cuál es el riesgo más urgente del caso y quién debe asumirlo?

## Material

| Recurso | Uso |
| --- | --- |
| `notebooks/01_tracking_mlop.ipynb` | Práctica MLOps sin resolver; 35–40 minutos. |
| `notebooks/01_tracking_mlop_solucion.ipynb` | Solución docente de MLOps. |
| `notebooks/02_agent_llmops.ipynb` | Práctica AgentOps/LLMOps sin resolver; 20–30 minutos. |
| `notebooks/02_agent_llmops_solucion.ipynb` | Solución docente de AgentOps/LLMOps. |
| `exercises/01_tracking_mlop/README.md` | Guía de alumno para el tracking clásico. |
| `exercises/02_agent_llmops/README.md` | Guía de alumno para trazas y evaluación. |
| `exercises/01_project_risks_and_tracking.md` | Entregable individual o por pareja. |
| `examples/s01_project_record.yaml` | Plantilla de la ficha de proyecto y riesgos. |
| `instructor/README.md` | Preparación y guion para el docente. |

## Convenciones de la semana

- En Free Edition cada notebook conserva su propio experimento; el nombre del
  *run* contiene el alias del estudiante, nunca su correo ni datos personales.
- Los secretos viven en Databricks Secrets o en la identidad del entorno; no
  se registran como parámetros, *tags*, artefactos ni salidas de trazas.
- Cada artefacto debe poder explicarse: finalidad, propietario, datos usados y
  criterio para pasar a la siguiente etapa.
- El modelo clásico, la aplicación de agente y la evaluación se observan desde
  el experimento del notebook para que se vea el ciclo completo; en producción
  se separarán por sistema y por permisos.

## Referencias técnicas

- [Experimentos de MLflow en Databricks](https://docs.databricks.com/aws/en/mlflow/experiments)
- [Tracking de modelos en Databricks](https://docs.databricks.com/aws/en/mlflow/tracking)
- [Trazas de agentes y LLMs en MLflow](https://mlflow.org/docs/latest/genai/tracing)
- [Evaluación de GenAI en MLflow](https://mlflow.org/docs/latest/genai/eval-monitor/)
