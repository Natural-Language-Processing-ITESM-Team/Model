# Model

Este repositorio contiene el modelo creado con el framework BERTopic. Además, incluye el conjunto de datos creado apartir de tweets extraídos de las cuentas oficiales del Tecnológico de Monterrey en Twitter.

## Descripción

Respecto a la etapa de modelación, se requería un modelo clasificador de topics (aprendizaje no supervisado), a continuación se explica el desarrollo del mismo. 

En la ciencia de datos, específicamente en los modelos de aprendizaje es de vital importancia tener data de calidad. Es por esto que el equipo pensó que la fuente principal de información para entrenar nuestro clasificador serían los tweets del Tecnológico de Monterrey. Aunque, esta no fue nuestra primera opción, ya que desafortunadamente Punto Azul no colaboró compartiéndonos información respecto a los servicios del TEC. Afortunadamente Twitter si lo hizo, y con su API fue posible extraer data para la creación de nuestro conjunto de datos.

Propiamente en el desarrollo del modelo, es momento de hablar de BERTopic, la cuál es una técnica de modelado de topics que permite utilizar modelos pre entrenados de HuggingFace. Esta última es una empresa estadounidense que desarrolla herramientas para crear aplicaciones utilizando el aprendizaje automático. Este framework es considerado por muchos el futuro del modelado de temas.

### Algoritmo

En síntesis, el algoritmo de BERTopic funciona de la siguiente manera: 
* Paso 1. Aprovecha las capacidades del lenguaje de modelos transformadores, es decir, por medio de embeddings comienza convirtiendo la data en representaciones vectoriales mediante el uso de un modelo transformador de oraciones. Nosotros utilizamos el modelo multilenguaje "sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2" de HuggingFace, ya que asigna oraciones a un espacio vectorial denso de 384 dimensiones y puede usarse para tareas como agrupación o búsqueda semántica. Más información en: [paraphrase-multilingual-MiniLM-L12-v2](https://huggingface.co/sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2).

* Paso 2. Se encarga de reducir la dimensionalidad con ayuda de algunas técnicas de aprendizaje automático; UMAP y Análisis de Componentes Principales (PCA) son las más comunes.

* Paso 3. Con ayuda de algoritmos de agrupamiento es posible la creación de clusters, donde cada uno de estos engloba un tema diferente. Nosotros utilizamos el algoritmo de agrupamiento mejorado HDBSCAN (el cuál extiende DBSCAN convirtiéndolo en un algoritmo de agrupamiento jerárquico) con el fin de encontrar tweets semánticos similares. 

* Paso 4. Se aplica CountVectorizer con el fin de tokenizar cada tema en una representación de bolsa de palabras (Bag-of-Words) para procesar los datos sin afectar las incrustaciones de entrada.

* Paso 5. Se calculan las palabras más representativas de cada topic con ayuda de un procedimiento TF-IDF basado en clases.

Finalmente, es importante decir que nosotros forzamos al algoritmo a obtener 5 topics, puesto que contamos con 5 motores de NLP. Si deseas saber más del funcionamiento de BERTopic o detalles de su implementación, aquí te dejamos el link a su documentación: [BERTopic](https://maartengr.github.io/BERTopic/index.html).

## Autor
[Abraham Gil Félix](https://www.linkedin.com/in/abraham-gil-f%C3%A9lix-955a4a1a9/)
