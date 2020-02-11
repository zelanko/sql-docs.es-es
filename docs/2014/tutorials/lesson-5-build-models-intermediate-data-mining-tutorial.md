---
title: 'Lección 5: generar modelos de red neuronal y de regresión logística (tutorial intermedio de minería de datos) | Microsoft Docs'
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- data mining [Analysis Services], tutorials
- neural networks
- tutorials [Data Mining]
- neural network model [Analysis Services]
ms.assetid: 42c3701a-1fd2-44ff-b7de-377345bbbd6b
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: daf554338a50a81f46d86a77bf04e770fcc2512e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63137450"
---
# <a name="lesson-5-building-neural-network-and-logistic-regression-models-intermediate-data-mining-tutorial"></a>Lección 5: Generar modelos de red neuronal y de regresión logística (Tutorial intermedio de minería de datos)
  
  
 El departamento de operaciones de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] está ocupado en un proyecto para mejorar la satisfacción del cliente con su centro de llamadas. Han contratado a un proveedor para administrar el centro de llamadas y proporcionar métricas sobre la efectividad del centro de llamadas, y le han solicitado el análisis de algunos datos preliminares que proporciona el proveedor. Ellos desean saber si hay algún resultado interesante. En particular, desean saber si los datos sugieren algún problema con el personal o métodos para mejorar la satisfacción del cliente.  
  
 El conjunto de datos es pequeño y solo cubre un período de 30 días en el funcionamiento del centro de llamadas. Los datos hacen un seguimiento del número de operadores nuevos y experimentados en cada turno, el número de llamadas entrantes, el número de pedidos y de problemas que se deben resolver y el tiempo promedio de espera de un cliente para que alguien responda a una llamada. Los datos también incluyen una métrica de calidad de servicio basada en la *tasa de abandono*, que es un indicador de la frustración del cliente.  
  
 Puesto que no cuenta con expectativas a priori sobre lo que mostrarán los datos, decide usar un modelo de red neuronal para explorar posibles correlaciones. En la exploración se suelen utilizar modelos de red neuronal que pueden analizar relaciones complejas entre muchas entradas y salidas.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En esta lección, usará el algoritmo de red neuronal para crear un modelo que tanto usted como el equipo de operaciones puedan utilizar para conocer las tendencias en los datos. Como parte de esta lección, intentará responder las siguientes preguntas:  
  
-   ¿Qué factores afectan a la satisfacción del cliente?  
  
-   ¿Qué puede realizar el centro de llamadas para mejorar la calidad de servicio?  
  
 A continuación, basándose en los resultados, creará un modelo de regresión logística que puede utilizar para las predicciones. El equipo de operaciones utilizará estas predicciones como ayuda para planear el funcionamiento del centro de llamadas.  
  
 En esta lección se incluyen los temas siguientes:  
  
-   [Agregar una vista del origen de datos para los datos del centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
-   [Crear un modelo y una estructura de red neuronal &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Explorar el modelo de centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
-   [Agregar un modelo de regresión logística a la estructura del centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
-   [Crear predicciones para los modelos del centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Agregar una vista del origen de datos para los datos del centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas las lecciones  
 [Lección 1: crear la solución intermedia de minería de datos &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lección 2: generar un escenario de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 3: generar un escenario de cesta de la compra &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 4: generar un escenario de agrupación en clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 Lección 5: Modelo de red neuronal y de regresión logística (tutorial intermedio de minería de datos)  
  
## <a name="see-also"></a>Consulte también  
 [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial intermedio de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
