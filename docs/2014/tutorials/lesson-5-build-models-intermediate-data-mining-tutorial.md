---
title: 'Lección 5: Creación de red neuronal y modelos de regresión logística (Tutorial de minería de datos intermedios) | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63137450"
---
# <a name="lesson-5-building-neural-network-and-logistic-regression-models-intermediate-data-mining-tutorial"></a>Lección 5: Creación de red neuronal y modelos de regresión logística (Tutorial de minería de datos intermedios)
  
  
 El departamento de operaciones de [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] está ocupado en un proyecto para mejorar la satisfacción del cliente con su centro de llamadas. Han contratado a un proveedor para administrar el centro de llamadas y proporcionar métricas sobre la efectividad del centro de llamadas, y le han solicitado el análisis de algunos datos preliminares que proporciona el proveedor. Ellos desean saber si hay algún resultado interesante. En particular, desean saber si los datos sugieren algún problema con el personal o métodos para mejorar la satisfacción del cliente.  
  
 El conjunto de datos es pequeño y solo cubre un período de 30 días en el funcionamiento del centro de llamadas. Los datos hacen un seguimiento del número de operadores nuevos y experimentados en cada turno, el número de llamadas entrantes, el número de pedidos y de problemas que se deben resolver y el tiempo promedio de espera de un cliente para que alguien responda a una llamada. Los datos también incluyen una métrica de calidad de servicio basada en la *tasa de abandono*, que es un indicador de la frustración del cliente.  
  
 Puesto que no cuenta con expectativas a priori sobre lo que mostrarán los datos, decide usar un modelo de red neuronal para explorar posibles correlaciones. En la exploración se suelen utilizar modelos de red neuronal que pueden analizar relaciones complejas entre muchas entradas y salidas.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En esta lección, usará el algoritmo de red neuronal para crear un modelo que tanto usted como el equipo de operaciones puedan utilizar para conocer las tendencias en los datos. Como parte de esta lección, intentará responder las siguientes preguntas:  
  
-   ¿Qué factores afectan a la satisfacción del cliente?  
  
-   ¿Qué puede realizar el centro de llamadas para mejorar la calidad de servicio?  
  
 A continuación, basándose en los resultados, creará un modelo de regresión logística que puede utilizar para las predicciones. El equipo de operaciones utilizará estas predicciones como ayuda para planear el funcionamiento del centro de llamadas.  
  
 En esta lección se incluyen los temas siguientes:  
  
-   [Agregar datos de una vista de datos del centro de llamadas del origen &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
-   [Crear una estructura de red neuronal y el modelo &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Explorar el modelo de centro de llamadas &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
-   [Adición de un modelo de regresión logística a la estructura de centro de llamadas &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
-   [Crear predicciones para los modelos de centro de llamadas &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/create-predictions-call-center-models-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Agregar datos de una vista de datos del centro de llamadas del origen &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/add-data-source-view-call-center-data-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas las lecciones  
 [Lección 1: Creación de la solución de minería de datos intermedios &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lección 2: Generar un escenario de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 3: Generar un escenario de cesta &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 4: Creación de una escenario de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 Lección 5: Red neuronal y el escenario de regresión logística (Tutorial de minería de datos intermedios)  
  
## <a name="see-also"></a>Vea también  
 [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial de minería de datos de datos intermedio &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
