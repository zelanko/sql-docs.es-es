---
title: Algoritmo de regresión lineal de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- algorithms [data mining]
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 50a4abb8-c0b0-4380-ba5e-c49b305b9d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df1b3616a85d93b4c5fa814ee759880077c03b8f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084042"
---
# <a name="microsoft-linear-regression-algorithm"></a>Algoritmo de regresión lineal de Microsoft
  El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una variación del algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] que ayuda a calcular una relación lineal entre una variable independiente y otra dependiente y, a continuación, utilizar esa relación para la predicción.  
  
 La relación toma la forma de una ecuación para la línea que mejor represente una serie de datos. Por ejemplo, la línea del siguiente diagrama muestra la mejor representación lineal de los datos.  
  
 ![Línea que modela un conjunto de datos](../media/linear-regression.gif "Línea que modela un conjunto de datos")  
  
 Cada punto de datos del diagrama tiene un error asociado con su distancia con respecto a la línea de regresión. Los coeficientes a y b de la ecuación de regresión ajustan el ángulo y la ubicación de la recta de regresión. Puede obtener la ecuación de regresión ajustando a y b hasta que la suma de los errores asociados a todos los puntos alcance su valor mínimo.  
  
 Hay otros tipos de regresión que utilizan varias variables y también hay métodos no lineales de regresión. Sin embargo, la regresión lineal es un método útil y conocido para modelar una respuesta a un cambio de algún factor subyacente.  
  
## <a name="example"></a>Ejemplo  
 Puede utilizar la regresión lineal para determinar una relación entre dos columnas continuas. Por ejemplo, puede utilizar la regresión lineal para calcular una línea de tendencias en los datos de fabricación o ventas. También podría utilizar la regresión lineal como precursor para el desarrollo de modelos de minería de datos más complejos, con el fin de evaluar las relaciones entre las columnas de datos.  
  
 Aunque hay muchas maneras de calcular la regresión lineal que no requieren herramientas de minería de datos, la ventaja de utilizar el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para esta tarea es que se calculan y se prueban automáticamente todas las posibles relaciones entre las variables. No tiene que seleccionar un método de cálculo, como por ejemplo para resolver los mínimos cuadrados. Sin embargo, la regresión lineal podría simplificar en exceso las relaciones en escenarios en los que varios factores afectan al resultado.  
  
## <a name="how-the-algorithm-works"></a>Cómo funciona el algoritmo  
 El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una variación del algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Al seleccionar el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , se invoca un caso especial del algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , con parámetros que restringen el comportamiento del algoritmo y requieren ciertos tipos de datos de entrada. Además, en un modelo de regresión lineal, el conjunto de datos completo se utiliza para calcular las relaciones en el paso inicial, mientras que en un modelo de árboles de decisión estándar los datos se dividen repetidamente en árboles o subconjuntos más pequeños.  
  
## <a name="data-required-for-linear-regression-models"></a>Datos requeridos para los modelos de regresión lineal  
 Cuando se preparan datos para utilizarse en un modelo de regresión lineal, se deben entender los requisitos del algoritmo determinado. Esto incluye saber cuántos datos se necesitan y cómo se utilizan. Los requisitos para este tipo de modelo son los siguientes:  
  
-   **Una columna de clave única** Cada modelo debe contener una columna numérica o de texto que identifique cada registro de forma única. No están permitidas las claves compuestas.  
  
-   **Una columna de predicción** Requiere al menos una columna de predicción. Se pueden incluir varios atributos de predicción en un modelo, pero deben ser tipos de datos numéricos continuos. No se puede utilizar un tipo de datos de fecha y hora como atributo de predicción aunque el almacenamiento nativo para los datos sea numérico.  
  
-   **Columnas de entrada** Las columnas de entrada deben contener datos numéricos continuos y se les debe asignar el tipo de datos adecuado.  
  
 Para obtener más información, vea la sección Requisitos de [Referencia técnica del algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm-technical-reference.md).  
  
## <a name="viewing-a-linear-regression-model"></a>Ver un modelo de regresión lineal  
 Para examinar el modelo, puede utilizar el **Visor de árboles de Microsoft**. La estructura de árbol de un modelo de regresión lineal es muy simple, con toda la información sobre la ecuación de regresión contenida en un nodo único. Para obtener más información, vea [Examinar un modelo usando el Visor de árboles de Microsoft](browse-a-model-using-the-microsoft-tree-viewer.md).  
  
 Si desea obtener información más detallada sobre la ecuación, también puede ver los coeficientes y otros detalles utilizando el [Visor de árbol de contenido genérico de Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
 En un modelo de regresión lineal, el contenido incluye metadatos, la fórmula de regresión y estadísticas sobre la distribución de los valores de entrada. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md).  
  
## <a name="creating-predictions"></a>Crear predicciones  
 Una vez procesado el modelo, los resultados se almacenan como un conjunto de estadísticas junto con la fórmula de regresión lineal, que se puede utilizar para calcular tendencias futuras. Para obtener ejemplos de consultas que se usan con un modelo regresión lineal, vea [Ejemplos de consultas de modelos de regresión lineal](linear-regression-model-query-examples.md).  
  
 Para obtener información general sobre cómo crear consultas con modelos de minería de datos, vea [Consultas de minería de datos](data-mining-queries.md).  
  
 Además de crear un modelo de regresión lineal seleccionando el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , si el atributo de predicción es un tipo de datos numéricos continuo, puede crear un modelo de árbol de decisión que contenga regresiones. En este caso, el algoritmo dividirá los datos cuando encuentre puntos de separación adecuados, pero en cambio creará una fórmula de regresión para algunas regiones de datos. Para obtener más información sobre los árboles de regresión en un modelo de árboles de decisión, vea [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md).  
  
## <a name="remarks"></a>Observaciones  
  
-   No se admite el uso del Lenguaje de marcado de modelos de predicción (PMML) para crear modelos de minería de datos.  
  
-   No admite la creación de dimensiones de minería de datos.  
  
-   Admite la obtención de detalles.  
  
-   Admite el uso de modelos de minería de datos OLAP.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining-algorithms-analysis-services-data-mining.md)   
 [Referencia técnica del algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm-technical-reference.md)   
 [Ejemplos de consultas de modelos de regresión lineal](linear-regression-model-query-examples.md)   
 [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;&#41;de minería de datos Analysis Services](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
