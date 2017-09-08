---
title: Algoritmo de red neuronal de Microsoft | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- training neural networks
- output neurons [Analysis Services]
- algorithms [data mining]
- neural network algorithms [Analysis Services]
- neurons [Analysis Services]
- classification algorithms [Analysis Services]
- neural networks
- multilayer perceptron network of neurons [Analysis Services]
- hidden neurons
- Back-Propagated Delta Rule network
- input neurons [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 61eb4861-8a6a-4214-a4b8-1dd278ad7a68
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 53869c8e03d3b4c289872351e59579d49aa193e2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-neural-network-algorithm"></a>Algoritmo de red neuronal de Microsoft
  El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una implementación de la popular arquitectura de red neuronal adaptable para el aprendizaje automático.  El algoritmo prueba cada posible estado del atributo de entrada con cada posible estado del atributo de predicción, y calcula las probabilidades de cada combinación según los datos de aprendizaje. Puede usar estas probabilidades para tareas de clasificación o regresión, así como para predecir un resultado en función de algunos atributos de entrada. También se puede usar una red neuronal para el análisis de asociación.  
  
 Cuando se crea un modelo de minería de datos con el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , puede incluir varias salidas y el algoritmo creará varias redes. El número de redes incluidas en un modelo de minería de datos depende del número de estados (o valores de atributo) de las columnas de entrada, así como del número de columnas de predicción que usa el modelo de minería de datos y el número de estados de dichas columnas.  
  
## <a name="example"></a>Ejemplo  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es útil para analizar datos de entrada complejos, como los datos de un proceso comercial o de producción, o problemas empresariales para los que hay una cantidad importante de datos de entrenamiento disponibles pero en los que no es fácil derivar reglas mediante otros algoritmos.  
  
 Los casos sugeridos para utilizar el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son:  
  
-   Análisis de comercialización y promoción, como medir el éxito de una promoción por correo directo o una campaña publicitaria en la radio.  
  
-   Predecir los movimientos de las acciones, la fluctuación de la moneda u otra información financiera con gran número de cambios a partir de los datos históricos.  
  
-   Analizar los procesos industriales y de producción.  
  
-   Minería de texto.  
  
-   Cualquier modelo de predicción que analice relaciones complejas entre muchas entradas y relativamente pocas salidas.  
  
## <a name="how-the-algorithm-works"></a>Cómo funciona el algoritmo  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] crea una red formada por hasta tres niveles de nodos (en ocasiones denominados *neuronas*). Estos niveles son el *nivel de entrada*, el *nivel oculto*y el *nivel de salida*.  
  
 **Nivel de entrada** : los nodos de entrada definen todos los valores de atributos de entrada para el modelo de minería de datos, así como sus probabilidades.  
  
 **Nivel oculto** : los nodos ocultos reciben entradas de los nodos de entrada y proporcionan salidas a los nodos de salida. El nivel oculto es donde se asignan pesos a las distintas probabilidades de las entradas. Un peso describe la relevancia o importancia de una entrada determinada para el nodo oculto. Cuanto mayor sea el peso asignado a una entrada, más importante será el valor de dicha entrada. Los pesos pueden ser negativos, lo que significa que la entrada puede desactivar, en lugar de activar, un resultado concreto.  
  
 **Nivel de salida** : los nodos de salida representan valores de atributo de predicción para el modelo de minería de datos.  
  
 Para obtener una explicación detallada sobre cómo se construyen y puntúan los niveles de entrada, los niveles de salida y los niveles ocultos, vea [Referencia técnica del algoritmo de red neuronal de Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="data-required-for-neural-network-models"></a>Datos requeridos para los modelos de red neuronal  
 El modelo de red neuronal debe contener una columna de clave, una o más columnas de entrada y una o más columnas de predicción.  
  
 Los modelos de minería de datos que usan el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] están muy influenciados por los valores que se especifican en los parámetros disponibles para el algoritmo. Los parámetros definen cómo se muestrean los datos, cómo se distribuyen o cómo se espera que estén distribuidos en cada columna, y cuándo se invoca la selección de características para limitar los valores usados en el modelo final.  
  
 Para obtener más información sobre cómo establecer parámetros para personalizar el comportamiento del modelo, vea [Referencia técnica del algoritmo de red neuronal de Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).  
  
## <a name="viewing-a-neural-network-model"></a>Ver un modelo de red neuronal  
 Para trabajar con los datos y ver cómo el modelo pone en correlación las entradas y salidas, puede usar el **Visor de redes neuronales de Microsoft**. Con este visor personalizado, puede filtrar los atributos de entrada y sus valores, y ver gráficamente cómo afectan a las salidas. La información sobre herramientas del visor muestra la probabilidad y la mejora respecto al modelo predictivo asociados a cada par de valores de entrada y de salida. Para obtener más información, vea [Examinar un modelo usando el Visor de redes neuronales de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md).  
  
 La manera más fácil de explorar la estructura del modelo consiste en usar el **Visor de árbol de contenido genérico de Microsoft**. Este visor le permitirá ver las entradas, las salidas y las redes creadas por el modelo, así como hacer clic en cualquier nodo para expandirlo y ver las estadísticas relacionadas con los niveles de entrada, los niveles de salida y los niveles ocultos de los nodos. Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
## <a name="creating-predictions"></a>Crear predicciones  
 Una vez procesado el modelo, puede usar la red y los pesos almacenados dentro de cada nodo para realizar predicciones. Un modelo de red neuronal admite el análisis de regresión, de asociación y de clasificación. Por lo tanto, el significado de cada predicción puede ser diferente. También puede consultar el propio modelo, revisar las correlaciones encontradas y recuperar las estadísticas relacionadas. Para obtener ejemplos de cómo crear consultas en un modelo de red neuronal, vea [Ejemplos de consultas de modelos de red neuronal](../../analysis-services/data-mining/neural-network-model-query-examples.md).  
  
 Para obtener información general sobre cómo crear una consulta en un modelo de minería de datos, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="remarks"></a>Comentarios  
  
-   No admite la obtención de detalles ni las dimensiones de minería de datos. Esto se debe a que la estructura de los nodos del modelo de minería de datos no tiene por qué corresponder directamente a los datos subyacentes.  
  
-   No admite la creación de modelos en el formato PMML (Lenguaje de marcado de modelos de predicción).  
  
-   Admite el uso de modelos de minería de datos OLAP.  
  
-   No admite la creación de dimensiones de minería de datos.  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica del algoritmo de red neuronal de Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de red neuronal &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Ejemplos de consultas de modelo de red neuronal](../../analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Algoritmo de regresión logística de Microsoft](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)  
  
  

