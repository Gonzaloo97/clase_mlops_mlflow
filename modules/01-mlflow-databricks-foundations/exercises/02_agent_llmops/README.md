# Guía del alumno — Práctica 02: AgentOps y LLMOps

## Qué vas a conseguir

Construirás un asistente didáctico mínimo para el caso cardiovascular de la
semana y observarás cómo MLflow guarda sus pasos como una traza. Después
evaluarás una propiedad concreta de sus respuestas con un *scorer* de código.

La práctica usa `USE_LLM = False`: enseña el flujo de AgentOps y LLMOps sin
consumir cuota de un endpoint. El agente no proporciona consejo clínico.

## Antes de empezar

1. Trabaja en el mismo Databricks Git Folder que usaste para la práctica 01.
2. Abre `notebooks/02_agent_llmops.ipynb`, la libreta sin resolver.
3. Ejecuta la instalación de MLflow sólo si el runtime lo requiere. Si se
   reinicia Python, vuelve a ejecutar las celdas desde imports.
4. Mantén `USE_LLM = False`. No instales `databricks-openai`, no pegues tokens
   ni inventes nombres de endpoints salvo que el docente indique la demo.

## Orden de trabajo

1. Revisa `COURSE_CONTEXT`. Es el único contexto que el agente puede usar;
   contiene información didáctica y un límite explícito de uso clínico.
2. Completa `route_question` con las tres rutas indicadas: `mlflow`, `security`
   y `risk`. Conserva el decorador `@mlflow.trace`.
3. Completa `retrieve_course_context` para devolver el texto asociado a la ruta.
4. Completa `course_agent` en este orden: ruta → contexto → respuesta
   determinista. Ejecuta las tres preguntas de prueba.
5. Abre **Experiments** en la barra lateral y selecciona una traza de
   `course_agent`. Identifica las trazas hijas de ruta y recuperación de
   contexto.
6. Completa `contains_expected_phrase` y llama a
   `mlflow.genai.evaluate(...)` con `EVALUATION_DATA`, `course_agent` y tu
   scorer.

## Qué debes observar en MLflow

La traza raíz debe contener la pregunta y la respuesta. Dentro de ella deben
aparecer los pasos `route_question` y `retrieve_course_context`. La evaluación
crea evidencia adicional para cada pregunta, pero aprobar el scorer sólo
demuestra que aparece una frase: no demuestra que una respuesta sea completa,
segura, cierta o útil.

## Demo real de LLM (sólo cuando lo indique el docente)

El docente puede activar `USE_LLM = True` en la libreta resuelta y consultar un
Foundation Model API visible en **Serving**. En ese caso inspecciona el span
adicional de LLM, su latencia y el uso de tokens. No es necesario ni obligatorio
configurarlo en tu cuenta Free Edition: la cuota, los endpoints disponibles y la
capacidad pueden variar.

## Problemas habituales

| Situación | Qué hacer |
| --- | --- |
| La respuesta no sigue la ruta esperada | Imprime el resultado de `route_question(question)` y comprueba las palabras clave y el orden de condiciones. |
| No aparece una traza | Vuelve a ejecutar las definiciones con `@mlflow.trace` y después una pregunta de prueba. |
| La evaluación falla | Revisa que `predict_fn=course_agent`, el nombre del scorer y la clave `must_include` coincidan con `EVALUATION_DATA`. |
| El endpoint no está disponible | Mantén `USE_LLM = False`; la práctica y el entregable siguen completos. |

## Qué entregar

Añade a la ficha común el identificador de una traza, el resultado de la
evaluación y una limitación concreta de `contains_expected_phrase`. Propón un
control que cubriría esa limitación, por ejemplo una prueba de seguridad,
latencia, recuperación de contexto o revisión humana.
