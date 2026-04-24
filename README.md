# Evaluación de Modelos de Traducción Automática Inglés-Español

## Descripción del proyecto

Este proyecto evalúa el desempeño de diferentes modelos de traducción automática para traducir textos del idioma inglés al español.

La comparación se realizó utilizando modelos disponibles en Hugging Face, aplicados sobre una muestra del dataset `Helsinki-NLP/opus_books`, específicamente en el par de idiomas `en-es`.

El objetivo principal fue analizar la calidad de las traducciones generadas y el tiempo de inferencia de cada modelo, utilizando la métrica BLEU como referencia principal.

---

## ¿Qué hace este proyecto?

El proyecto realiza las siguientes tareas:

- Carga un dataset de traducción inglés-español desde Hugging Face.
- Extrae una muestra de 100 ejemplos.
- Traduce los textos en inglés al español usando distintos modelos.
- Compara las traducciones generadas con las traducciones de referencia.
- Calcula la métrica BLEU para medir la calidad de traducción.
- Mide el tiempo total y promedio de inferencia de cada modelo.
- Compara el rendimiento entre modelos de diferentes tamaños.

---

## Herramientas utilizadas

El proyecto fue desarrollado en Python, utilizando principalmente las siguientes herramientas y librerías:

- Python
- Google Colab / Jupyter Notebook
- Hugging Face Transformers
- Hugging Face Datasets
- Evaluate
- SacreBLEU
- PyTorch
- Pandas
- SentencePiece
- Accelerate

---

## Dataset utilizado

Se utilizó el dataset:

```text
Helsinki-NLP/opus_books
```

Subset utilizado:

```text
en-es
```

Este dataset contiene fragmentos de libros alineados en diferentes idiomas. En este proyecto se utilizó el par inglés-español, por lo que el contenido trabajado corresponde principalmente a textos narrativos y literarios.

Para mantener una comparación uniforme entre los modelos, se seleccionó una muestra de:

```text
100 ejemplos
```

---

## Modelos evaluados

Se evaluaron dos familias de modelos de traducción automática, cada una con dos variantes de tamaño diferente:

| Familia | Modelo | Tamaño | Descripción |
|---|---|---:|---|
| M2M100 | `facebook/m2m100_418M` | 418M | Modelo multilingüe many-to-many |
| M2M100 | `facebook/m2m100_1.2B` | 1.2B | Variante más grande de M2M100 |
| NLLB-200 | `facebook/nllb-200-distilled-600M` | 600M | Modelo multilingüe optimizado y más ligero |
| NLLB-200 | `facebook/nllb-200-1.3B` | 1.3B | Modelo de mayor tamaño enfocado en calidad |

---

## Instalación de dependencias

Antes de ejecutar el notebook, instala las librerías necesarias:

```bash
pip install transformers datasets evaluate sentencepiece sacrebleu accelerate
```

---

## Cómo ejecutar el proyecto

1. Clona este repositorio:

```bash
git clone https://github.com/tu-usuario/tu-repositorio.git
```

2. Entra a la carpeta del proyecto:

```bash
cd tu-repositorio
```

3. Abre el notebook:

```bash
jupyter notebook Traductor.ipynb
```

También puedes ejecutarlo directamente en Google Colab.

4. Ejecuta las celdas en orden.

5. El notebook realizará los siguientes pasos:

   - Instalación de dependencias.
   - Importación de librerías.
   - Verificación de GPU.
   - Carga del dataset.
   - Selección de la muestra.
   - Ejecución de los modelos.
   - Cálculo de BLEU.
   - Comparación de resultados.

---

## Métrica de evaluación

La métrica principal utilizada fue:

```text
BLEU - Bilingual Evaluation Understudy
```

BLEU mide la similitud entre la traducción generada por el modelo y una traducción de referencia.

Su escala va de 0 a 100:

- Un valor más alto indica mayor similitud con la traducción de referencia.
- Un valor más bajo indica menor coincidencia textual.

Aunque BLEU es útil para comparar modelos, también se realizó una revisión manual de ejemplos para observar la coherencia, naturalidad y fidelidad de las traducciones.

---

## Resultados obtenidos

| Modelo | Tamaño | BLEU | Tiempo total (s) | Tiempo promedio (s) |
|---|---:|---:|---:|---:|
| `facebook/m2m100_418M` | 418M | 25.3779 | 97.5173 | 0.9752 |
| `facebook/m2m100_1.2B` | 1.2B | 28.1347 | 138.9679 | 1.3897 |
| `facebook/nllb-200-distilled-600M` | 600M | 27.2594 | 66.1931 | 0.6619 |
| `facebook/nllb-200-1.3B` | 1.3B | 29.0251 | 115.3063 | 1.1531 |

---

## Análisis de resultados

El modelo con mejor puntuación BLEU fue:

```text
facebook/nllb-200-1.3B
```

Este modelo obtuvo un BLEU de `29.0251`, lo que indica que generó las traducciones más cercanas a las referencias del dataset.

El modelo más rápido fue:

```text
facebook/nllb-200-distilled-600M
```

Este obtuvo un tiempo promedio de `0.6619` segundos por traducción, siendo la opción más eficiente en términos de velocidad.

En general, los modelos de mayor tamaño obtuvieron mejores resultados de calidad, pero también requirieron más tiempo de procesamiento. Sin embargo, el modelo `nllb-200-distilled-600M` presentó un buen equilibrio entre calidad y eficiencia.

---

## Observaciones

Durante la revisión manual de ejemplos se observó que los modelos tuvieron mejor desempeño en oraciones completas con suficiente contexto.

Las traducciones fueron más naturales y coherentes cuando el texto de entrada tenía una estructura clara. Sin embargo, algunos errores aparecieron en títulos, nombres propios, encabezados o fragmentos con poco contexto.

Esto demuestra que, además de utilizar métricas automáticas como BLEU, también es importante revisar ejemplos manualmente para evaluar la calidad real de las traducciones.

---

## Conclusión

El mejor modelo en calidad de traducción fue:

```text
facebook/nllb-200-1.3B
```

El modelo más eficiente en velocidad fue:

```text
facebook/nllb-200-distilled-600M
```

Por tanto:

- Si la prioridad es obtener la mayor calidad posible, la mejor opción es `nllb-200-1.3B`.
- Si la prioridad es lograr un equilibrio entre calidad y rapidez, la mejor opción es `nllb-200-distilled-600M`.

---

## Caso de uso empresarial

Un posible caso de uso empresarial para este proyecto sería la traducción automática de documentos, catálogos, correos, artículos o materiales institucionales dirigidos a públicos hispanohablantes.

Por ejemplo, una empresa internacional podría utilizar un modelo de traducción automática para traducir documentación de soporte técnico desde inglés hacia español, reduciendo el tiempo de trabajo manual y facilitando el acceso a la información para clientes o colaboradores.

En escenarios donde se requiera procesar grandes volúmenes de texto rápidamente, el modelo `nllb-200-distilled-600M` sería una alternativa eficiente. Para documentos donde la calidad final sea más importante, `nllb-200-1.3B` sería una mejor opción.

---

## Estructura sugerida del repositorio

```text
.
├── Traductor.ipynb
├── README.md
└── resultados/
    └── resumen_modelos.csv
```

---

## Autor

Proyecto desarrollado como parte de una evaluación de modelos de traducción automática utilizando modelos de lenguaje disponibles en Hugging Face.
