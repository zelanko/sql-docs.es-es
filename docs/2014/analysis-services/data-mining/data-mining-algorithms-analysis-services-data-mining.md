---
title: Algoritmos de minería de datos (Analysis Services - minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- clustering [Data Mining]
- learning algorithms
- data mining [Analysis Services], models
- algorithms [data mining]
- mining models [Analysis Services], algorithms
- inductive learning
- mining models [Analysis Services], creating
- data mining [Analysis Services], algorithms
- machine learning algorithms [Analysis Services]
ms.assetid: ed1fc83b-b98c-437e-bf53-4ff001b92d64
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 082241af377c8817c3adbc394a46f1ebc7d6a4e3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085142"
---
# <a name="data-mining-algorithms-analysis-services---data-mining"></a>Algoritmos de minería de datos (Analysis Services: Minería de datos)
  Un *algoritmo de minería de datos* es un conjunto de heurísticas y cálculos que crea un modelo de minería de datos. Para crear un modelo, el algoritmo analiza primero los datos proporcionados, en busca de tipos específicos de patrones o tendencias. El algoritmo usa los resultados de este análisis para definir los parámetros óptimos para la creación del modelo de minería de datos. A continuación, estos parámetros se aplican en todo el conjunto de datos para extraer patrones procesables y estadísticas detalladas.  
  
 El modelo de minería de datos que crea un algoritmo a partir de los datos puede tomar diversas formas, incluyendo:  
  
-   Un conjunto de clústeres que describe cómo se relacionan los casos de un conjunto de datos.  
  
-   Un árbol de decisión que predice un resultado y que describe cómo afectan a este los distintos criterios.  
  
-   Un modelo matemático que predice las ventas.  
  
-   Un conjunto de reglas que describen cómo se agrupan los productos en una transacción, y las probabilidades de que dichos productos se adquieran juntos.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona varios algoritmos para su uso en las soluciones de minería de datos. Estos algoritmos son implementaciones de algunas de las metodologías más conocidas usadas en la minería de datos. Todos los algoritmos de minería de datos de Microsoft se pueden personalizar y son totalmente programables, bien mediante las API proporcionadas o bien mediante los componentes de minería de datos de SQL Server Integration Services.  
  
 También puede utilizar algoritmos de terceros que cumplan con OLE DB para minería de datos de especificación, o bien desarrollar algoritmos personalizados que se pueden registrar como servicios y, a continuación, se usa dentro del marco de minería de datos de SQL Server.  
  
## <a name="choosing-the-right-algorithm"></a>Elegir el algoritmo correcto  
 La elección del mejor algoritmo para una tarea analítica específica puede ser un desafío. Aunque puede usar diferentes algoritmos para realizar la misma tarea, cada uno de ellos genera un resultado diferente, y algunos pueden generar más de un tipo de resultado. Por ejemplo, puede usar el algoritmo Árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no solo para la predicción, sino también como una forma de reducir el número de columnas de un conjunto de datos, ya que el árbol de decisión puede identificar las columnas que no afectan al modelo de minería de datos final.  
  
### <a name="choosing-an-algorithm-by-type"></a>Elegir un algoritmo por tipo  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye los siguientes tipos de algoritmos:  
  
-   **Algoritmos de clasificación** , que predicen una o más variables discretas, basándose en los demás atributos del conjunto de datos.  
  
-   **Los algoritmos de regresión** predecir una o más variables continuas, como pérdidas o ganancias, basándose en otros atributos del conjunto de datos.  
  
-   **Algoritmos de segmentación** , que dividen los datos en grupos, o clústeres, de elementos que tienen propiedades similares.  
  
-   **Algoritmos de asociación** , que buscan correlaciones entre diferentes atributos de un conjunto de datos. La aplicación más común de esta clase de algoritmo es la creación de reglas de asociación, que pueden usarse en un análisis de la cesta de compra.  
  
-   **Algoritmos de análisis de secuencias** resumir las secuencias frecuentes o episodios en los datos, como un flujo de la ruta de acceso Web.  
  
 Sin embargo, no hay ninguna razón por la que deba limitarse a un algoritmo en sus soluciones. Los analistas experimentados usarán a veces un algoritmo para determinar las entradas más eficaces (es decir, variables) y luego aplicarán un algoritmo diferente para predecir un resultado concreto basado en esos datos. Minería de datos de SQL Server le permite generar varios modelos en una estructura de minería de datos única, por lo que dentro de una solución de minería de datos podría usar un algoritmo de agrupación en clústeres, un modelo de árboles de decisión y un modelo Bayes naive para obtener distintas vistas de los datos. También puede usar varios algoritmos dentro de una única solución para realizar tareas independientes: por ejemplo, podría usar la regresión para obtener predicciones financieras, y un algoritmo de red neuronal para realizar un análisis de los factores que influyen en las ventas.  
  
### <a name="choosing-an-algorithm-by-task"></a>Elegir un algoritmo por tarea  
 Con el fin de ayudarle a seleccionar un algoritmo para su uso con una tarea específica, la tabla siguiente proporciona sugerencias para los tipos de tareas para las que se usa normalmente cada algoritmo.  
  
|Ejemplos de tareas|Algoritmos de Microsoft que se pueden usar|  
|-----------------------|---------------------------------|  
|**Predecir un atributo discreto**<br /><br /> Marcar los clientes de una lista de posibles compradores como clientes con buenas o malas perspectivas.<br /><br /> Calcular la probabilidad de que un servidor genere un error en los próximos 6 meses.<br /><br /> Clasificar la evolución de los pacientes y explorar los factores relacionados.|[Algoritmo de árboles de decisión de Microsoft](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo Bayes naive de Microsoft](microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo de clústeres de Microsoft](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo de red neuronal de Microsoft](microsoft-neural-network-algorithm.md)|  
|**Predecir un atributo continuo**<br /><br /> Pronosticar las ventas del año próximo.<br /><br /> Predecir los visitantes del sitio a partir de tendencias históricas y estacionales proporcionadas.<br /><br /> Generar una puntuación de riesgo a partir de datos demográficos.|[Algoritmo de árboles de decisión de Microsoft](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo de serie temporal de Microsoft](microsoft-time-series-algorithm.md)<br /><br /> [Algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm.md)|  
|**Predecir una secuencia**<br /><br /> Realizar un análisis clickstream del sitio web de una empresa.<br /><br /> Analizar los factores que dan como resultado errores en el servidor.<br /><br /> Capturar y analizar secuencias de actividades durante las visitas de pacientes externos, para formular las prácticas recomendadas en las actividades comunes.|[Algoritmo de clústeres de secuencia de Microsoft](microsoft-sequence-clustering-algorithm.md)|  
|**Buscar grupos de elementos comunes en las transacciones**<br /><br /> Usar el análisis de la cesta de la compra para determinar la posición del producto.<br /><br /> Sugerir a un cliente la compra de productos adicionales.<br /><br /> Analizar los datos de una encuesta a los visitantes a un evento, para descubrir qué actividades o stands estaban correlacionados con el fin de programar actividades futuras.|[Algoritmo de asociación de Microsoft](microsoft-association-algorithm.md)<br /><br /> [Algoritmo de árboles de decisión de Microsoft](microsoft-decision-trees-algorithm.md)|  
|**Buscar grupos de elementos similares**<br /><br /> Crear grupos de pacientes con perfiles de riesgo en función de atributos como datos demográficos y comportamientos.<br /><br /> Analizar usuarios mediante patrones de búsqueda y compra de productos.<br /><br /> Identificar servidores con características de uso similares.|[Algoritmo de clústeres de Microsoft](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo de clústeres de secuencia de Microsoft](microsoft-sequence-clustering-algorithm.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
 En la tabla siguiente se incluyen vínculos a recursos de aprendizaje para cada uno de los algoritmos de minería de datos que se proporcionan en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
|||  
|-|-|  
|**Descripción básica del algoritmo**|Explica lo que hace que el algoritmo y cómo funciona, y describe los posibles escenarios empresariales donde podría resultar útil.|  
||[Algoritmo de asociación de Microsoft](microsoft-association-algorithm.md)<br /><br /> [Algoritmo de clústeres de Microsoft](microsoft-clustering-algorithm.md)<br /><br /> [Algoritmo de árboles de decisión de Microsoft](microsoft-decision-trees-algorithm.md)<br /><br /> [Algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm.md)<br /><br /> [Algoritmo de regresión logística de Microsoft](microsoft-logistic-regression-algorithm.md)<br /><br /> [Algoritmo Bayes naive de Microsoft](microsoft-naive-bayes-algorithm.md)<br /><br /> [Algoritmo de red neuronal de Microsoft](microsoft-neural-network-algorithm.md)<br /><br /> [Algoritmo de clústeres de secuencia de Microsoft](microsoft-sequence-clustering-algorithm.md)<br /><br /> [Algoritmo de serie temporal de Microsoft](microsoft-time-series-algorithm.md)|  
|**Referencia técnica**|Proporciona detalles técnicos sobre la implementación del algoritmo, con referencias académicas según sea necesario. Muestra los parámetros que pueden establecerse para controlar el comportamiento del algoritmo y personalizar los resultados en el modelo. Describe los requisitos de los datos y proporciona sugerencias de rendimiento si es posible.|  
||[Referencia técnica del algoritmo de asociación de Microsoft](microsoft-association-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de clústeres de Microsoft](microsoft-clustering-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de árboles de decisión de Microsoft](microsoft-decision-trees-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de regresión logística de Microsoft](microsoft-logistic-regression-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo Bayes naive de Microsoft](microsoft-naive-bayes-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de red neuronal de Microsoft](microsoft-neural-network-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de clústeres de secuencia de Microsoft](microsoft-sequence-clustering-algorithm-technical-reference.md)<br /><br /> [Referencia técnica del algoritmo de serie temporal de Microsoft](microsoft-time-series-algorithm-technical-reference.md)|  
|**Contenido del modelo**|Explica cómo está estructurada la información dentro de cada tipo de modelo de minería de datos, y cómo interpretar la información almacenada en cada uno de los nodos.|  
||[Contenido del modelo de minería de datos para los modelos de asociación &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-association-models-analysis-services-data-mining.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de regresión logística &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-logistic-regression-models.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos Bayes naive &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de red neuronal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-sequence-clustering-models.md)<br /><br /> [Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)|  
|**Consultas de minería de datos**|Proporciona varias consultas que se pueden usar con cada tipo de modelo. Los ejemplos incluyen consultas de contenido que le proporcionan más información sobre los patrones del modelo, así como consultas de predicción para ayudarle a crear predicciones basadas en esos patrones.|  
||[Ejemplos de consultas del modelo de asociación](association-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de agrupación en clústeres](clustering-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de árboles de decisión](decision-trees-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de regresión lineal](linear-regression-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de regresión logística](logistic-regression-model-query-examples.md)<br /><br /> [Ejemplos de consultas del modelo Bayes naive](naive-bayes-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de red neuronal](neural-network-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de clústeres de secuencia](sequence-clustering-model-query-examples.md)<br /><br /> [Ejemplos de consultas de modelos de serie temporal](time-series-model-query-examples.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|**Tema**|**Descripción**|  
|---------------|---------------------|  
|Determinar el algoritmo usado por un modelo de minería de datos|[Consultar los parámetros usados para crear un modelo de minería de datos](query-the-parameters-used-to-create-a-mining-model.md)|  
|Crear un algoritmo complementario personalizado|[Algoritmos de complemento](plugin-algorithms.md)|  
|Explorar un modelo con un visor específico para algoritmos|[Visores de modelos de minería de datos](data-mining-model-viewers.md)|  
|Ver el contenido de un modelo con un formato de tabla genérico|[Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)|  
|Obtener información sobre cómo configurar los datos y usar algoritmos para crear modelos|[Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-structures-analysis-services-data-mining.md)<br /><br /> [Modelos de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-models-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de minería de datos](data-mining-tools.md)  
  
  
