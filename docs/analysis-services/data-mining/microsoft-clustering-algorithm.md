---
title: "Algoritmo de cl&#250;steres de Microsoft | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "algoritmos de segmentación [Analysis Services]"
  - "vecino más cercano [Minería de datos]"
  - "clústeres [Minería de datos]"
  - "clústeres [Analysis Services]"
  - "relaciones [Analysis Services], clústeres"
  - "algoritmos [minería de datos]"
  - "algoritmos de clasificación [Analysis Services]"
  - "conjuntos de datos [Analysis Services]"
  - "algoritmos de clústeres [Analysis Services]"
ms.assetid: 92a1e67e-f46e-4960-99b2-4d20f6192fbd
caps.latest.revision: 62
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 62
---
# Algoritmo de cl&#250;steres de Microsoft
  El algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de *segmentación* o *clústeres* que itera en los casos de un conjunto de datos para agruparlos en clústeres que contengan características similares. Estas agrupaciones son útiles para la exploración de datos, la identificación de anomalías en los datos y la creación de predicciones.  
  
 Los modelos de agrupación en clústeres identifican las relaciones en un conjunto de datos que no se podrían derivar lógicamente a través de la observación casual. Por ejemplo, puede adivinar fácilmente que las personas que se desplazan a sus trabajos en bicicleta no viven, por lo general, a gran distancia de sus lugares de trabajo. Sin embargo, el algoritmo puede encontrar otras características que no son evidentes acerca de los trabajadores que se desplazan en bicicleta. En el siguiente diagrama, el clúster A representa los datos sobre las personas que suelen conducir hasta el trabajo, en tanto que el clúster B representa los datos sobre las personas que van hasta allí en bicicleta.  
  
 ![Patrón de clústeres de tendencias de conmutador](../../analysis-services/data-mining/media/clustering-example.gif "Patrón de clústeres de tendencias de conmutador")  
  
 El algoritmo de clústeres se diferencia de otros algoritmos de minería de datos, como el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , en que no se tiene que designar una columna de predicción para generar un modelo de agrupación en clústeres. El algoritmo de clústeres entrena el modelo de forma estricta a partir de las relaciones que existen en los datos y de los clústeres que identifica el algoritmo.  
  
## Ejemplo  
 Considere un grupo de personas que comparten información demográfica similar y que adquieren productos similares de la empresa [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] . Este grupo de personas representa un clúster de datos. En una base de datos pueden existir varios clústeres como éstos. Mediante la observación de las columnas que forman un clúster, puede ver con mayor claridad la forma en que los registros de un conjunto de datos se relacionan entre sí.  
  
## Cómo funciona el algoritmo  
 El algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] identifica primero las relaciones de un conjunto de datos y genera una serie de clústeres basándose en ellas. Un gráfico de dispersión es una forma útil de representar visualmente el modo en que el algoritmo agrupa los datos, tal como se muestra en el siguiente diagrama. El gráfico de dispersión representa todos los casos del conjunto de datos; cada caso es un punto del gráfico. Los clústeres agrupan los puntos del gráfico e ilustran las relaciones que identifica el algoritmo.  
  
 ![Gráfico de dispersión de casos en un conjunto de datos](../../analysis-services/data-mining/media/clustering-plot.png "Gráfico de dispersión de casos en un conjunto de datos")  
  
 Después de definir los clústeres, el algoritmo calcula el grado de perfección con que los clústeres representan las agrupaciones de puntos y, a continuación, intenta volver a definir las agrupaciones para crear clústeres que representen mejor los datos. El algoritmo establece una iteración en este proceso hasta que ya no es posible mejorar los resultados mediante la redefinición de los clústeres.  
  
 Puede personalizar el funcionamiento del algoritmo seleccionando una técnica de agrupación en clústeres, limitando el número máximo de clústeres o cambiando la cantidad de soporte que se requiere para crear un clúster. Para obtener más información, vea [Referencia técnica del algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md). Este algoritmo incluye dos métodos populares de agrupación en clústeres: el método de agrupación en clústeres k-means y el método de maximización de la expectativa.  
  
## Datos requeridos para los modelos de agrupación en clústeres  
 Al preparar los datos para su uso en el entrenamiento de un modelo de agrupación en clústeres, conviene comprender qué requisitos son imprescindibles para el algoritmo concreto, incluidos el volumen de datos necesario y la forma en que estos datos se utilizan.  
  
 Los requisitos para un modelo de agrupación en clústeres son los siguientes:  
  
-   **Una columna de una sola clave** : cada modelo debe contener una columna numérica o de texto que identifique cada registro de manera única. No están permitidas las claves compuestas.  
  
-   **Columnas de entrada** Cada modelo debe tener al menos una columna de entrada que contenga los valores que se utilizan para generar los clústeres. Puede tener tantas columnas de entrada como desee, pero dependiendo del número de valores existentes en cada columna, la adición de columnas adicionales podría aumentar el tiempo necesario para entrenar el modelo.  
  
-   **Una columna de predicción opcional** El algoritmo no necesita una columna de predicción para generar el modelo, pero puede agregar una columna de predicción de casi cualquier tipo de datos. Los valores de la columna de predicción se pueden tratar como entradas del modelo de agrupación en clústeres, o se puede especificar que solo se utilicen para las predicciones. Por ejemplo, si desea predecir los ingresos del cliente agrupando en clústeres de acuerdo con datos demográficos como la región o la edad, se deben especificar los ingresos como **PredictOnly** y agregar todas las demás columnas, como la región o la edad, como entradas.  
  
 Para obtener información más detallada sobre los tipos de contenido y los tipos de datos compatibles con los modelos de agrupación en clústeres, vea la sección Requisitos de [Referencia técnica del algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
## Ver un modelo de agrupación en clústeres  
 Para explorar el modelo, puede utilizar el **Visor de clústeres de Microsoft**. Cuando se observa un modelo de agrupación en clústeres, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] presenta los clústeres en un diagrama que muestra las relaciones existentes entre ellos, además de un perfil detallado de cada clúster, una lista de los atributos que diferencian cada clúster de los demás, y las características de todo el conjunto de datos de entrenamiento. Para obtener más información, vea [Examinar un modelo usando el Visor de clústeres de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md).  
  
 Si desea obtener más detalles, puede examinar el modelo en el [Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). El contenido almacenado para el modelo incluye la distribución para todos los valores de cada nodo, la probabilidad de cada clúster y otros datos. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
## Crear predicciones  
 Una vez entrenado el modelo, los resultados se almacenan como un conjunto de patrones que se puede explorar o utilizar para realizar predicciones.  
  
 Puede crear consultas para devolver predicciones sobre si los nuevos datos se ajustan a los clústeres que se han detectado, o para obtener estadísticas descriptivas sobre los clústeres.  
  
 Para obtener información sobre cómo crear consultas en un modelo de minería de datos, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md). Para obtener ejemplos de cómo usar las consultas con un modelo de agrupación en clústeres, vea [Ejemplos de consultas de modelos de agrupación en clústeres](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## Comentarios  
  
-   Admite el uso del Lenguaje de marcado de modelos de predicción (PMML) para crear modelos de minería de datos.  
  
-   Admite la obtención de detalles.  
  
-   Admite el uso de modelos de minería de datos OLAP y la creación de dimensiones de minería de datos.  
  
## Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referencia técnica del algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)   
 [Ejemplos de consultas de modelos de agrupación en clústeres](../../analysis-services/data-mining/clustering-model-query-examples.md)  
  
  