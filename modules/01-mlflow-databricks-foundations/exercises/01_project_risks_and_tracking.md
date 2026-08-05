# Práctica 01 — Evidencia antes de producción

**Duración:** 60 minutos · **Modalidad:** individual o por parejas

## Objetivo

Transformar un entrenamiento de notebook en una evidencia operable: un *run*
comparable, un registro de riesgos como artefacto y una primera traza con
evaluación de agente.

## Antes de empezar

1. Abre tu notebook en Databricks Free Edition. MLflow crea automáticamente el
   experimento del notebook cuando inicias un run; ábrelo desde **Experiments**
   en la barra lateral.
2. Elige un alias de equipo que no revele información personal, por ejemplo
   `pareja-07`.
3. No pegues claves, tokens, correos, datos de pacientes ni contenido sensible
   en ninguna celda. MLflow registra lo que le entregas.

## Parte A — Tracking de MLOps (30 min)

1. Ejecuta `notebooks/01_tracking_mlop.ipynb` con tu alias. Reutiliza el caso
   de clasificación cardiovascular de `data/raw/heart.csv`; no lo uses para
   decisiones clínicas.
2. Cambia **una** configuración que afecte al modelo (por ejemplo,
   `max_depth` o `min_samples_leaf`) y lanza un segundo *run*.
3. Compara `test_f1`, `test_recall` y `test_roc_auc` desde la UI de MLflow. No declares un
   ganador sólo con una métrica: explica qué información falta.
4. Adapta `examples/s01_project_record.yaml` a tu caso y registra su contenido
   como artefacto JSON o YAML. Incluye al menos tres riesgos, un propietario y
   una mitigación por riesgo.

## Parte B — AgentOps y LLMOps (20 min)

1. Ejecuta `notebooks/02_agent_llmops.ipynb` con `USE_LLM = False`.
2. Abre una traza de `course_agent` y localiza sus pasos `route_question` y
   `retrieve_course_context`. Escribe qué paso habría permitido depurar una
   respuesta incorrecta.
3. Ejecuta la evaluación. Identifica un caso que el *scorer*
   `contains_expected_phrase` considera correcto y explica por qué ese criterio
   no basta para autorizar producción.
4. Sólo si el docente lo indica, habilita el endpoint de Foundation Model y
   repite una pregunta. No cambies la configuración de autenticación.

## Parte C — Entregable y debrief (10 min)

Entrega una ficha corta (Markdown, YAML o enlace a su artefacto de MLflow) con:

- alias de equipo, nombre y enlace del experimento;
- nombres de los dos *runs* y sus métricas;
- decisión provisional y la evidencia que todavía falta;
- tres riesgos priorizados y su propietario;
- enlace o identificador de una traza y el límite del *scorer* usado.

## Rúbrica (10 puntos)

| Criterio | Puntos |
| --- | ---: |
| Dos runs comparables, con parámetros y métricas visibles | 3 |
| Registro de riesgos concreto y enlazado como artefacto | 3 |
| Lectura correcta de una traza y de su límite de evaluación | 2 |
| Decisión prudente, sin secretos ni afirmaciones de uso clínico | 2 |

## Extensión si terminas antes

Propón un *scorer* adicional que detecte un riesgo que el actual no cubre
(por ejemplo, latencia, cita de fuentes, lenguaje inseguro o ausencia de una
respuesta de incertidumbre). Describe la entrada, la salida y un contraejemplo
que podría engañarlo.
