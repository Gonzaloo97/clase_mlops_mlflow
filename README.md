# Operación de Modelos — MUIAAP (ICAI)

Material práctico para la asignatura de Operación de Modelos del Máster
Universitario en Inteligencia Artificial Aplicada. El curso sigue un único hilo:
pasar de un experimento reproducible a un servicio observable, seguro y
desplegable.

## Semana 01: MLflow en Databricks

El material activo de la primera semana está en
[`modules/01-mlflow-databricks-foundations/`](modules/01-mlflow-databricks-foundations/).
Parte de las dos sesiones previstas en el calendario de ICAI:

| Sesión | Duración | Foco | Evidencia |
| --- | ---: | --- | --- |
| Clase 1 | 2 h | Prototipo frente a producción; ciclo de vida de modelos y de aplicaciones con LLM | Mapa de ciclo de vida y riesgos iniciales |
| Clase 2 | 1 h + 1 h | Demo de MLflow en Databricks; tracking, selección, Registry, API local, trazas y evaluación | Inicio de ficha de proyecto y evidencia en MLflow |

El ciclo completo de ML se termina como una práctica autónoma de 2–3 horas
adicionales para no comprimir artificialmente los conceptos en la sesión.

Las prácticas usan el servidor MLflow gestionado de Databricks y cubren tres
vistas del mismo ciclo de evidencia. En Free Edition cada notebook mantiene su
propio experimento, por lo que los *runs* de MLOps y las trazas/evaluaciones de
AgentOps/LLMOps se consultan en sus respectivos notebooks:

1. **MLOps clásico:** datos, runs, artefactos, modelos, selección, test, Registry
   y una API local observable que carga el pickle ganador.
2. **AgentOps:** trazas de la aplicación, enrutado y herramientas.
3. **LLMOps:** evaluación reproducible basada en datos y un scorer de código.

El Registry usa Unity Catalog. El despliegue de ML es deliberadamente local al
driver (`127.0.0.1`) y efímero: enseña contrato, health check, errores y
telemetría sin depender de infraestructura de pago. No es un endpoint público
ni persistente.

## Uso en Databricks

1. Cada estudiante usa su workspace personal de Databricks Free Edition. MLflow
   registra los runs en el experimento asociado a cada notebook, sin permisos
   compartidos, siguiendo la guía de
   [preparación de la semana 01](modules/01-mlflow-databricks-foundations/instructor/README.md).
2. Abre el repositorio como Databricks Git Folder. Así los notebooks encuentran
   el caso existente `data/raw/heart.csv`. Si los subes manualmente, sube también
   el CSV y actualiza `DATASET_PATH`.
3. Entrega las versiones sin resolver `01_tracking_mlops.ipynb` y
   `02_agent_llmops.ipynb`. Conserva los pares `_solucion.ipynb` para el docente
   y la corrección.

Las credenciales no se escriben en los notebooks. Dentro de Databricks se usa
la autenticación configurada por el entorno; fuera del workspace deben
configurarse las variables de Databricks de forma segura.

## Material histórico

Los notebooks de la carpeta `notebooks/` se conservan como referencia de un
curso anterior. Usan dependencias y patrones de MLflow anteriores y no son la
secuencia recomendada para el curso de ICAI. No los modifiques ni los ejecutes
en clase sin adaptarlos al runtime actual de Databricks.

## Estructura

```text
modules/
  01-mlflow-databricks-foundations/
    notebooks/       # Notebooks Databricks guiados
    exercises/       # Trabajo independiente y rúbrica
    examples/        # Plantillas y evidencias esperadas
    instructor/      # Preparación del workspace y guion docente
```
