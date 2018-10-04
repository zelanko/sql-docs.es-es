---
title: 'Lección 4: Generar una escenario (Tutorial de minería de datos intermedios) de clústeres de secuencia | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e276d4a2b44c8d0fdc6be6787f58e359e4c15d5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122575"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>Lección 4: Generar un escenario de agrupación en clústeres de secuencia (Tutorial intermedio de minería de datos)
  El departamento de marketing de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] desea saber cómo los clientes se mueven a través de la [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] sitio Web. La empresa cree que existe un patrón según el cual los clientes incluyen productos en las cestas de la compra. Desean analizar el orden de secuencias de compra para obtener información sobre el modo en que los clientes agregan los elementos relacionados a la cesta de la compra. Posteriormente, esta información se puede utilizar para mejorar el flujo del sitio web y propiciar que los clientes adquieran productos adicionales.  
  
 Después de completar las tareas de esta lección, habrá creado un modelo de minería de datos que use el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)] para predecir cuál será el siguiente artículo que los clientes incluirán en la cesta de la compra. Experimentará con dos versiones del modelo: una que analiza solo el orden de productos en la cesta y otra que contiene datos demográficos adicionales del cliente para la agrupación en clústeres. Finalmente, utilizará los modelos para crear predicciones que puede utilizar para recomendar productos a los clientes.  
  
 Para completar las tareas de la lección, usará la estructura de minería de datos market basket que creó en [lección 3: creación de un escenario de cesta &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md). Esta lección contiene las siguientes tareas:  
  
-   [Creación de una estructura del modelo de minería de datos de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [Procesar el modelo de agrupación en clústeres de secuencia](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [Explorar el modelo de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Crear un modelo de clúster de secuencia relacionado &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Crear predicciones en una modelo de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Creación de una estructura del modelo de minería de datos de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas las lecciones  
 [Lección 1: Crear la solución de minería de datos intermedios &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lección 2: Creación de un escenario de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 3: Generar un escenario de cesta &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 Lección 4: Escenario de agrupación en clústeres de secuencia (tutorial intermedio de minería de datos)  
  
 [Lección 5: Generar modelos de regresión logística y Red neuronal &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tutorial de minería de datos básicos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial de minería de datos de datos intermedio &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
