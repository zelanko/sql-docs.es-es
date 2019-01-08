---
title: Creación de un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining models, creating
- forecasting [data mining]
- mining models, creating
- clustering [data mining]
- association [data mining]
- data modeling [data mining]
- estimation
- classification [data mining]
ms.assetid: 804b7db3-1f6a-4f73-a81d-bbe02520d7c6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5d7efc9df277f609bf53ffb49f2253a937f45a4b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394468"
---
# <a name="creating-a-data-mining-model"></a>Crear un modelo de minería de datos
  Modelado de datos es el paso de minería de datos donde se generan patrones y tendencias aplicando *algoritmos* a los datos. Después, puede utilizar esos patrones para el análisis, o para realizar predicciones.  
  
 Los Complementos de minería de datos para Office admiten la minería de datos a través de asistentes que facilitan la creación de modelos. Los asistentes analizan los datos, identifican las correlaciones, calculan la importancia estadística de todas las variables y seleccionan automáticamente el mejor modelo.  
  
 Aunque esta funcionalidad es tan eficaz como las herramientas proporcionadas por minería de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], la combinación de los asistentes y la conocida interfaz de Excel facilita la tarea crear, modificar y utilizar la minería de datos.  
  
## <a name="advanced-data-mining"></a>Avanzados (Minería de datos)  
 Los asistentes avanzados permiten crear nuevos modelos de minería de datos, basados en datos almacenados en Excel, mediante uno de los algoritmos de minería de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
### <a name="create-mining-structure"></a>Crear estructura de minería de datos  
 El Asistente para crear estructuras de minería de datos le permite generar una nueva estructura de minería de datos que podrá usar como base para varios modelos de minería de datos. El asistente le da la opción de reservar una parte de los datos y usarla como conjunto de prueba; de este modo, podrá evaluar todos los modelos que usan los mismos datos de acuerdo con un estándar de pruebas coherente.  
  
 [Crear estructura de minería de datos &#40;complementos de minería de datos de SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
### <a name="add-model-to-structure"></a>Agregar modelo a estructura  
 El Asistente para agregar modelos a una estructura le permite elegir una estructura de minería de datos existente y crear un nuevo modelo de minería de datos para ella. Puede agregar varios modelos de minería de datos a una estructura, cambiar los parámetros o elegir distintos algoritmos de minería de datos, y personalizar la salida.  
  
 [Agregar modelo a estructura &#40;datos complementos de minería de datos para Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md)  
  
## <a name="analyze-key-influencers-analyze"></a>Analizar influenciadores clave (Analizar)  
 Elija una columna o valor de salida de interés y el algoritmo analizará todos los datos de entrada para identificar los factores que ejercen mayor influencia en el destino. Opcionalmente, puede crear un informe que compare dos valores, de modo que pueda ver cómo cambian los influenciadores.  
  
 El **analizar Influenciadores clave** herramienta usa el algoritmo Bayes Naïve de Microsoft.  
  
 [Analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
  
## <a name="associate-data-mining"></a>Asociar (Minería de datos)  
 El **asociar** asistente genera un modelo de asociación que detecta asociaciones entre los elementos que aparecen en varias transacciones: por ejemplo, en el análisis de cesta.  
  
 [Asistente para asociación &#40;cliente de minería de datos para Excel&#41;](associate-wizard-data-mining-client-for-excel.md)  
  
## <a name="classify-data-mining"></a>Clasificar (Minería de datos)  
 El **clasificar** asistente genera un modelo de clasificación que analiza los factores que contribuyeron a un resultado de destino. Puede utilizar varios algoritmos con este asistente, incluidos los de árboles de decisión, Bayes naive y redes neuronales.  
  
 [Asistente para clasificar &#40;datos complementos de minería de datos para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="cluster-data-mining"></a>Clúster (Minería de datos)  
 El **clúster** asistente genera un modelo de agrupación en clústeres que detecta grupos de filas que comparten características similares. Agrupación en clústeres (a veces denominado *segmentación*) es una técnica de aprendizaje que resulta muy útil al tratar de comprender los patrones y agrupaciones en nuevos datos.  
  
 El algoritmo de clústeres de secuencia de Microsoft admite varias modalidades de agrupación en clústeres Expectation maximization (EM) y mediana-K  
  
 [Asistente para clúster &#40;datos complementos de minería de datos para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md).  
  
## <a name="detect-categories-analyze"></a>Detectar categorías (Analizar)  
 El **detectar categorías** herramienta le permite agregar cualquier conjunto de datos y aplicar la agrupación en clústeres para buscar agrupaciones de datos. Es útil para buscar similitudes y crear grupos para analizarlos en detalle.  
  
 El **detectar categorías** herramienta usa el algoritmo Microsoft Clustering.  
  
 [Detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
## <a name="estimate-data-mining"></a>Estimación (Minería de datos)  
 El Asistente para estimación de datos genera un modelo de estimación que extrae patrones de datos y los usa para predecir valores numéricos, de fecha o de hora continuos. Utiliza el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 [Asistente para estimación &#40;datos complementos de minería de datos para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="fill-from-example-analyze"></a>Rellenar desde ejemplo (Analizar)  
 El **rellenar desde ejemplo** herramienta le ayuda a imputar valores ausentes. Proporcione algunos ejemplos de cómo deben ser los valores ausentes, y la herramienta creará patrones basados en todos los datos de la tabla; a continuación, recomendará nuevos valores basados en patrones de los datos.  
  
 El **rellenar desde ejemplo** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Rellenar desde ejemplo &#40;herramientas de análisis de tabla para Excel&#41;](fill-from-example-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-analyze"></a>Pronóstico (Analizar)  
 El **previsión** herramienta toma los datos que cambian con el tiempo y predice valores futuros.  
  
 El **previsión** herramienta usa el algoritmo de serie temporal de Microsoft.  
  
 [Previsión &#40;herramientas de análisis de tabla para Excel&#41;](forecast-table-analysis-tools-for-excel.md)  
  
## <a name="forecast-data-mining"></a>Pronóstico (Minería de datos)  
 El **previsión** asistente genera un modelo de pronóstico que detecta patrones en una serie de celdas y, a continuación, pronostica valores adicionales.  
  
 [Asistente para pronóstico &#40;datos complementos de minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
## <a name="highlight-exceptions-analyze"></a>Resaltar excepciones (Analizar)  
 El **Resaltar excepciones** herramienta analiza patrones en una tabla de datos y busca filas y valores que no se ajustan al patrón. Seguidamente, puede revisarlos, corregirlos y volver a ejecutar el modelo o marcar valores para acciones posteriores.  
  
 El **Resaltar excepciones** herramienta usa el algoritmo Microsoft Clustering.  
  
 [Resaltar excepciones &#40;herramientas de análisis de tabla para Excel&#41;](highlight-exceptions-table-analysis-tools-for-excel.md)  
  
## <a name="prediction-calculator-analyze"></a>Cálculo de predicción (Analizar)  
 Esta herramienta crea un modelo que analiza los factores que producen los resultados buscados, y después predice un resultado para cualquier nueva entrada, en función de criterios derivados de estos patrones. También genera una hoja de cálculo interactiva de toma de decisiones que permite puntuar nuevas entradas. También puede crear una versión impresa de la hoja de cálculo de puntuaciones para su uso sin conexión.  
  
 El **cálculo de predicción** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Cálculo de predicción &#40;herramientas de análisis de tabla para Excel&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-goal-seek-analyze"></a>Escenario: Buscar objetivo (Analizar)  
 En el **Buscar objetivo** herramienta, especifique un valor de destino y la herramienta identifica los factores subyacentes que deben cambiar para alcanzar dicho destino. Por ejemplo, si sabe que debe aumentar la satisfacción de las llamadas en un 20 %, puede pedir al modelo que prediga los factores que deben cambiar para producir ese objetivo.  
  
 El **Buscar objetivo** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 detalles  
  
 [Escenario Buscar objetivo &#40;herramientas de análisis de tabla para Excel&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="scenario-what-if-scenario-analyze"></a>Escenario: Escenario y si (Analizar)  
 El **el análisis de hipótesis** herramienta complementa el **Buscar objetivo** herramienta. Con esta herramienta, se introduce el valor que se desea cambiar y el modelo predice si el cambio será suficiente para obtener el resultado deseado. Por ejemplo, podría solicitar al modelo que infiera si la adición de un operador de llamadas adicional incrementaría la satisfacción del cliente en un punto.  
  
 El **hipótesis** herramienta usa el algoritmo de regresión logística de Microsoft.  
  
 [Escenario y si &#40;herramientas de análisis de tabla para Excel&#41;](what-if-scenario-table-analysis-tools-for-excel.md)  
  
## <a name="shopping-basket-analysis-analyze"></a>Análisis de la cesta de compras (Analizar)  
 El **análisis de cesta de la compra** herramienta crea grupos de productos que se suelen comprar juntos, para identificar patrones que se pueden usar en las ventas cruzadas o ventas cruzadas arriba. También genera informes basados en el precio y el costo de paquetes de productos relacionados, para ayudar a la toma de decisiones.  
  
 También puede utilizar esta herramienta para los eventos que ocurren juntos con frecuencia, los factores que dan como resultado un diagnóstico o para cualquier otro posible conjunto de causas y resultados.  
  
 El **análisis de cesta de la compra** herramienta usa el algoritmo Microsoft Association.  
  
 [Análisis de cesta &#40;herramientas de análisis de tabla para Excel&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)  
  
## <a name="see-also"></a>Vea también  
 [Exploración y limpieza de datos](exploring-and-cleaning-data.md)   
 [Validar modelos y usar modelos para la predicción &#40;datos complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Implementar y ampliar modelos de minería de datos &#40;datos complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
