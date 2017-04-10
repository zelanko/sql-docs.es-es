---
title: "Algoritmo de regresi&#243;n log&#237;stica de Microsoft | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "algoritmos de regresión logística [Analysis Services]"
  - "algoritmos [minería de datos]"
  - "algoritmos de red neuronal [Analysis Services]"
  - "algoritmos de regresión [Analysis Services]"
ms.assetid: 3dd54d07-1c3b-4b87-b7f0-b962ed8cf844
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 22
---
# Algoritmo de regresi&#243;n log&#237;stica de Microsoft
  La regresión logística es una técnica estadística conocida que se usa para modelar los resultados binarios.  
  
 Existen varias implementaciones de regresión logística en la investigación estadística, que utilizan diferentes técnicas de aprendizaje. El algoritmo de Regresión logística de [!INCLUDE[msCoName](../../includes/msconame-md.md)] se ha implementado utilizando una variación del algoritmo de Red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Este algoritmo comparte muchas de las cualidades de las redes neurales pero es más fácil de entrenar.  
  
 Una de las ventajas de la regresión logística es que el algoritmo es muy flexible, puede tomar cualquier tipo de entrada y admite varias tareas analíticas diferentes:  
  
-   Usar datos demográficos para realizar predicciones sobre los resultados, como el riesgo de contraer una determinada enfermedad.  
  
-   Explorar y ponderar los factores que contribuyen a un resultado. Por ejemplo, buscar los factores que influyen en los clientes para volver a visitar un establecimiento.  
  
-   Clasificar los documentos, el correo electrónico u otros objetos que tengan muchos atributos.  
  
## Ejemplo  
 Imagine un grupo de personas que comparten información demográfica parecida y que adquieren productos de la empresa Adventure Works. Al modelar los datos para relacionarlos con un resultado concreto, como la compra de un producto de destino, podrá ver cómo contribuye la información demográfica a la probabilidad de que alguien adquiera dicho producto de destino.  
  
## Cómo funciona el algoritmo  
 La regresión logística es un método estadístico conocido que se usa para determinar la contribución de varios factores a un par de resultados. La implementación de Microsoft usa una red neuronal modificada para modelar las relaciones entre las entradas y los resultados. Se mide el efecto de cada entrada en el resultado y se ponderan las diversas entradas en el modelo acabado. El nombre regresión logística procede del hecho de que la curva de los datos se comprime mediante una transformación logística para minimizar el efecto de los valores extremos. Para obtener más información sobre la implementación y cómo personalizar el algoritmo, vea [Referencia técnica del algoritmo de regresión logística de Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## Datos requeridos para los modelos de regresión logística  
 Al preparar los datos para su uso en el entrenamiento de un modelo de regresión logística, conviene comprender qué requisitos son imprescindibles para el algoritmo concreto, incluidos el volumen de datos necesario y la forma en que estos datos se utilizan.  
  
 Los requisitos para un modelo de regresión logística son los siguientes:  
  
 **Una columna de una sola clave** : cada modelo debe contener una columna numérica o de texto que identifique cada registro de manera única. No están permitidas las claves compuestas.  
  
 **Columnas de entrada** : cada modelo debe tener al menos una columna de entrada que contenga los valores que se utilizan como factores en el análisis. Puede tener tantas columnas de entrada como desee, pero dependiendo del número de valores existentes en cada columna, la adición de columnas adicionales podría aumentar el tiempo necesario para entrenar el modelo.  
  
 **Al menos una columna de predicción** : el modelo debe contener al menos una columna de predicción de cualquier tipo de datos, incluidos datos numéricos continuos. Los valores de la columna de predicción también se pueden tratar como entradas del modelo, o se puede especificar que solo se utilicen para las predicciones. No se admiten tablas anidadas en las columnas de predicción, pero se pueden usar como entradas.  
  
 Para obtener información más detallada sobre los tipos de contenido y los tipos de datos compatibles con los modelos de regresión logística, vea la sección Requisitos de [Referencia técnica del algoritmo de regresión logística de Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).  
  
## Ver un modelo de regresión logística  
 Para explorar el modelo, puede usar el Visor de redes neuronales de Microsoft o el Visor de árbol de contenido genérico de Microsoft.  
  
 Cuando se ve el modelo con el Visor de redes neuronales de Microsoft, Analysis Services muestra los factores que contribuyen a un resultado determinado, clasificados por su importancia. Puede elegir un atributo y los valores que desea comparar. Para obtener más información, vea [Examinar un modelo usando el Visor de redes neuronales de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 Si desea obtener más información, puede examinar los detalles del modelo con el Visor de árbol de contenido genérico de Microsoft. El contenido de un modelo de regresión logística incluye un nodo marginal que muestra todas las entradas usadas para el modelo y las subredes de los atributos de predicción. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de regresión logística &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining model content for logistic regression models.md).  
  
## Crear predicciones  
 Una vez entrenado el modelo, puede crear consultas en el contenido del modelo para obtener los coeficientes de regresión y otros detalles, o puede usar el modelo para realizar predicciones.  
  
-   Para obtener información general sobre cómo crear consultas en un modelo de minería de datos, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
-   Para obtener ejemplos de consultas en un modelo de regresión logística, vea [Ejemplos de consultas de modelos de agrupación en clústeres](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## Comentarios  
  
-   No admite la obtención de detalles. Esto se debe a que la estructura de nodos del modelo de minería de datos no tiene por qué corresponder directamente a los datos subyacentes.  
  
-   No admite la creación de dimensiones de minería de datos.  
  
-   Admite el uso de modelos de minería de datos OLAP.  
  
-   No admite el uso del Lenguaje de marcado de modelos de predicción (PMML) para crear modelos de minería de datos.  
  
## Vea también  
 [Contenido del modelo de minería de datos para los modelos de regresión logística &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining model content for logistic regression models.md)   
 [Referencia técnica del algoritmo de regresión logística de Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [Ejemplos de consultas de modelos de regresión logística](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)  
  
  