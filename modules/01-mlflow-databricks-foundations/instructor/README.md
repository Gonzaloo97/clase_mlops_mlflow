# Preparación docente — Semana 01 (Databricks Free Edition)

## Objetivo operativo

La práctica está diseñada para que cada estudiante o pareja use su workspace
personal de Databricks Free Edition. No necesita un cluster administrado, un
experimento compartido, permisos de grupo ni un endpoint de pago. MLflow guarda
los *runs*, trazas y evaluaciones en el experimento asociado a cada notebook.

El objetivo no es desplegar ni registrar un modelo: es hacer visible la
evidencia que necesitaríamos para tomar esas decisiones en semanas posteriores.

## Lista de comprobación (hacer antes de clase)

1. Envía al alumnado el enlace de registro de Databricks Free Edition y pide que
   accedan a su workspace antes de la sesión. Free Edition es un entorno
   serverless con cuota; deja un margen para que se active el compute.
2. Comparte este repositorio. Cada estudiante puede importarlo como Databricks
   Git Folder. Así los notebooks encuentran el caso existente `data/raw/heart.csv`.
   Si se suben manualmente, sube también el CSV y actualiza `DATASET_PATH`.
3. Entrega los dos notebooks sin resolver y conserva los pares `_solucion.ipynb`
   para la demostración y la corrección. Prueba las soluciones desde una cuenta
   Free Edition. Ejecuta sólo las
   secciones deterministas; confirma que aparece el panel **Experiments** y que
   se crea un experimento de notebook automáticamente.
4. No presupongas que todos tienen un endpoint de Foundation Model disponible.
   `USE_LLM = False` es el modo obligatorio y produce las trazas de herramientas
   y el flujo de evaluación. Para enseñar el span de LLM real, realiza una
   demostración breve desde tu cuenta: en **Serving** copia el nombre de un
   Foundation Model API de chat que esté visible, instala `databricks-openai`,
   asígnalo a `MODEL_ENDPOINT` y ejecuta una sola pregunta. La solución indica
   cómo inspeccionar su latencia y uso de tokens en la traza.
5. No repartas tokens personales. Dentro de un notebook de Databricks la
   autenticación del entorno es suficiente para los servicios autorizados. No
   deben aparecer secretos, correos o datos sensibles en celdas, artefactos,
   parámetros ni trazas.

## Guion de la clase práctica (60 min)

| Minutos | Acción | Pregunta que guía la discusión |
| ---: | --- | --- |
| 0–5 | Localiza el experimento del notebook en la UI y explica *experiment*, *run*, artefacto y traza. | ¿Qué se pierde si sólo compartimos un notebook? |
| 5–20 | Ejecuta `01_tracking_mlop_solucion.ipynb` con dos configuraciones. | ¿Qué decisión se puede defender con F1, recall y el artefacto de riesgos? |
| 20–30 | Filtra y compara los dos runs del propio notebook. | ¿Qué dato adicional pedirías antes de elegir? |
| 30–45 | Ejecuta el modo determinista de `02_agent_llmops_solucion.ipynb` e inspecciona el árbol de la traza. | ¿Qué herramienta o paso explica la respuesta? |
| 45–55 | Muestra una única llamada a un Foundation Model API desde tu cuenta y después ejecuta el *scorer* de código. | ¿Qué falla puede detectar este *scorer* y cuál no? |
| 55–60 | Presenta el entregable y los criterios de aceptación. | ¿Cuál es el riesgo que debe escalarse antes de la semana 02? |

## Decisiones pedagógicas

- El modo determinista es intencionado: permite enseñar observabilidad y
  evaluación sin depender de coste, cuota o disponibilidad de un LLM.
- Cada alumno tiene un experimento propio. Para comparar resultados en clase,
  pide que compartan capturas de la tabla de runs o los valores de la ficha; no
  solicites acceso a sus workspaces personales.
- Una llamada real al endpoint es una demo de producto, no un requisito para
  aprobar la práctica. El alumnado debe poder reproducir el entregable sin
  consumir tokens.
- Free Edition es excelente para aprender el ciclo. Antes de producción, los
  experimentos, permisos, retención y datos de trazas deben diseñarse por
  sistema y riesgo, con gobernanza adicional.

## Referencias de configuración

- [Databricks Free Edition: capacidades y registro](https://docs.databricks.com/aws/en/getting-started/free-edition)
- [Límites de Free Edition](https://docs.databricks.com/aws/en/getting-started/free-edition-limitations)
- [Tracking de modelos en Databricks](https://docs.databricks.com/aws/en/mlflow/tracking)
- [Trazas de agentes y LLMs](https://docs.databricks.com/aws/en/mlflow3/genai/tracing/)
