# Guía del alumno — Práctica 01: tracking de MLOps

## Qué vas a conseguir

Crearás dos *runs* comparables para el caso de clasificación cardiovascular que
ya existe en el repositorio. Cada *run* contendrá parámetros, F1, recall, ROC
AUC, una tarjeta de datos y un registro de riesgos en MLflow.

El resultado es evidencia didáctica para operar un modelo: **no** es un sistema
clínico ni autoriza una decisión sobre pacientes.

## Antes de abrir la libreta

1. Entra en tu workspace personal de Databricks Free Edition y espera a que el
   compute serverless esté disponible.
2. Abre este repositorio como Databricks Git Folder. Es la opción recomendada
   porque mantiene disponible `data/raw/heart.csv`.
3. Abre `notebooks/01_tracking_mlop.ipynb`, la versión sin resolver. No copies
   ni ejecutes `01_tracking_mlop_solucion.ipynb` durante la práctica.
4. Si subiste la libreta manualmente, sube también `heart.csv` a Files y cambia
   `DATASET_PATH` por su ubicación. No sustituyas el dataset por información
   real de pacientes.

## Orden de trabajo

1. Ejecuta la celda de instalación sólo si MLflow no está disponible o tiene
   versión menor que 3.1. Si Databricks pide reiniciar Python, hazlo y vuelve a
   comenzar desde la celda de imports.
2. Sustituye los `TODO` de configuración por un alias no personal y por valores
   válidos de `max_depth` y `min_samples_leaf`.
3. Completa la tarjeta de datos. Explica que el caso procede del CSV histórico
   del repositorio y anota límites que impiden cualquier uso clínico.
4. Completa tres riesgos. Todos necesitan impacto, propietario y mitigación.
   Incluye al menos: uso clínico indebido, datos/representatividad y secretos o
   datos sensibles en logs.
5. Completa el bloque de MLflow: tags, parámetros, dos artefactos JSON y las
   tres métricas de prueba.
6. Ejecuta el entrenamiento una primera vez. Anota el nombre y el identificador
   del *run* en la ficha de proyecto.
7. Cambia **una sola** decisión de modelo y `RUN_LABEL`; ejecuta de nuevo el
   entrenamiento. Completa la celda de comparación con `mlflow.search_runs()`.

## Cómo comprobar tu trabajo

En la barra lateral del notebook abre **Experiments**. Debes ver dos *runs* en
el experimento de ese notebook. Cada uno debe mostrar:

- nombre con el alias del equipo, sin correo ni nombre completo;
- parámetros del clasificador y `test_f1`, `test_recall`, `test_roc_auc`;
- `governance/dataset_card.json` y `governance/risk_register.json` en
  artefactos;
- ningún token, dato personal o texto sensible.

## Problemas habituales

| Situación | Qué hacer |
| --- | --- |
| `FileNotFoundError` al leer el CSV | Comprueba que abriste un Git Folder y que `DATASET_PATH` apunta a `data/raw/heart.csv`; si subiste la libreta manualmente, actualiza la ruta al archivo que subiste. |
| No aparece un experimento | Ejecuta de nuevo la celda que contiene `mlflow.start_run()` y abre el icono **Experiments** del notebook. |
| No hay capacidad de compute | Free Edition aplica cuota. Espera al reinicio de capacidad y conserva tu libreta; no cambies a datos reales ni crees recursos de pago. |
| Un run tiene peor métrica | No es un error: úsalo para comparar la decisión y justificar qué evidencia adicional necesitarías. |

## Qué entregar

Completa la ficha común de
[`s01_project_record.yaml`](../../examples/s01_project_record.yaml) y añade el
enlace o identificador de los dos *runs*, sus métricas, una decisión provisional
y los tres riesgos. La solución se revisa por evidencia y razonamiento, no por
obtener una métrica concreta.
