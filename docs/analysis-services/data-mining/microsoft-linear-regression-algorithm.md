---
title: Algoritmo de regresión lineal de Microsoft | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 50a4abb8-c0b0-4380-ba5e-c49b305b9d22
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 15fd60a8cf05e501fda781e76fd716a45c0df1ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="microsoft-linear-regression-algorithm"></a>Algoritmo de regresión lineal de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una variación del algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] que ayuda a calcular una relación lineal entre una variable independiente y otra dependiente y, a continuación, utilizar esa relación para la predicción.  
  
 La relación toma la forma de una ecuación para la línea que mejor represente una serie de datos. Por ejemplo, la línea del siguiente diagrama muestra la mejor representación lineal de los datos.  
  
 ![Una línea que modela un conjunto de datos](../../analysis-services/data-mining/media/linear-regression.gif "una línea que modela un conjunto de datos")  
  
 Cada punto de datos del diagrama tiene un error asociado con su distancia con respecto a la línea de regresión. Los coeficientes a y b de la ecuación de regresión ajustan el ángulo y la ubicación de la recta de regresión. Puede obtener la ecuación de regresión ajustando a y b hasta que la suma de los errores asociados a todos los puntos alcance su valor mínimo.  
  
 Hay otros tipos de regresión que utilizan varias variables y también hay métodos no lineales de regresión. Sin embargo, la regresión lineal es un método útil y conocido para modelar una respuesta a un cambio de algún factor subyacente.  
  
## <a name="example"></a>Ejemplo  
 Puede utilizar la regresión lineal para determinar una relación entre dos columnas continuas. Por ejemplo, puede utilizar la regresión lineal para calcular una línea de tendencias en los datos de fabricación o ventas. También podría utilizar la regresión lineal como precursor para el desarrollo de modelos de minería de datos más complejos, con el fin de evaluar las relaciones entre las columnas de datos.  
  
 Aunque hay muchas maneras de calcular la regresión lineal que no requieren herramientas de minería de datos, la ventaja de utilizar el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para esta tarea es que se calculan y se prueban automáticamente todas las posibles relaciones entre las variables. No tiene que seleccionar un método de cálculo, como por ejemplo para resolver los mínimos cuadrados. Sin embargo, la regresión lineal podría simplificar en exceso las relaciones en escenarios en los que varios factores afectan al resultado.  
  
## <a name="how-the-algorithm-works"></a>Cómo funciona el algoritmo  
 El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una variación del algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Al seleccionar el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se invoca un caso especial del algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , con parámetros que restringen el comportamiento del algoritmo y requieren ciertos tipos de datos de entrada. Además, en un modelo de regresión lineal, el conjunto de datos completo se utiliza para calcular las relaciones en el paso inicial, mientras que en un modelo de árboles de decisión estándar los datos se dividen repetidamente en árboles o subconjuntos más pequeños.  
  
## <a name="data-required-for-linear-regression-models"></a>Datos requeridos para los modelos de regresión lineal  
 Cuando se preparan datos para utilizarse en un modelo de regresión lineal, se deben entender los requisitos del algoritmo determinado. Esto incluye saber cuántos datos se necesitan y cómo se utilizan. Los requisitos para este tipo de modelo son los siguientes:  
  
-   **Una columna de una sola clave** : cada modelo debe contener una columna numérica o de texto que identifique cada registro de manera única. No están permitidas las claves compuestas.  
  
-   **Una columna de predicción** . Se requiere al menos una columna de predicción. Se pueden incluir varios atributos de predicción en un modelo, pero deben ser tipos de datos numéricos continuos. No se puede utilizar un tipo de datos de fecha y hora como atributo de predicción aunque el almacenamiento nativo para los datos sea numérico.  
  
-   **Columnas de entrada** Deben contener datos numéricos continuos y se les debe asignarse el tipo de datos adecuado.  
  
 Para obtener más información, vea la sección Requisitos de [Referencia técnica del algoritmo de regresión lineal de Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md).  
  
## <a name="viewing-a-linear-regression-model"></a>Ver un modelo de regresión lineal  
 Para examinar el modelo, puede utilizar el **Visor de árboles de Microsoft**. La estructura de árbol de un modelo de regresión lineal es muy simple, con toda la información sobre la ecuación de regresión contenida en un nodo único. Para obtener más información, vea [Examinar un modelo usando el Visor de árboles de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md).  
  
 Si desea obtener información más detallada sobre la ecuación, también puede ver los coeficientes y otros detalles utilizando el [Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
 En un modelo de regresión lineal, el contenido incluye metadatos, la fórmula de regresión y estadísticas sobre la distribución de los valores de entrada. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions"></a>Crear predicciones  
 Una vez procesado el modelo, los resultados se almacenan como un conjunto de estadísticas junto con la fórmula de regresión lineal, que se puede utilizar para calcular tendencias futuras. Para obtener ejemplos de consultas que se usan con un modelo regresión lineal, vea [Ejemplos de consultas de modelos de regresión lineal](../../analysis-services/data-mining/linear-regression-model-query-examples.md).  
  
 Para obtener información general sobre cómo crear consultas con modelos de minería de datos, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
 Además de crear un modelo de regresión lineal seleccionando el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , si el atributo de predicción es un tipo de datos numéricos continuo, puede crear un modelo de árbol de decisión que contenga regresiones. En este caso, el algoritmo dividirá los datos cuando encuentre puntos de separación adecuados, pero en cambio creará una fórmula de regresión para algunas regiones de datos. Para obtener más información sobre los árboles de regresión en un modelo de árboles de decisión, vea [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).  
  
## <a name="remarks"></a>Comentarios  
  
-   No admite el uso del Lenguaje de marcado de modelos de predicción (PMML) para crear modelos de minería de datos.  
  
-   No admite la creación de dimensiones de minería de datos.  
  
-   Admite la obtención de detalles.  
  
-   Admite el uso de modelos de minería de datos OLAP.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referencia técnica del algoritmo de regresión lineal de Microsoft](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [Ejemplos de consultas de modelo de regresión lineal](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [Contenido del modelo de minería de datos para los modelos de regresión lineal & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
