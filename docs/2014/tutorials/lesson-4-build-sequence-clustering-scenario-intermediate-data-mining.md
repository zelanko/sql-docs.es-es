---
title: 'Lección 4: generar un escenario de agrupación en clústeres de secuencia (tutorial intermedio de minería de datos) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- sequence clustering algorithms [Analysis Services]
- tutorials [Data Mining]
ms.assetid: 63436bbd-0f73-4012-b6f1-358c81e4d92a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d34125b7b750daa1da25c9e8788172b5d9ca2c35
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62710607"
---
# <a name="lesson-4-building-a-sequence-clustering-scenario-intermediate-data-mining-tutorial"></a>Lección 4: Generar un escenario de agrupación en clústeres de secuencia (Tutorial intermedio de minería de datos)
  El departamento de marketing de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] desea saber cómo se mueven los clientes por el sitio web de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] . La empresa cree que existe un patrón según el cual los clientes incluyen productos en las cestas de la compra. Desean analizar el orden de secuencias de compra para obtener información sobre el modo en que los clientes agregan los elementos relacionados a la cesta de la compra. Posteriormente, esta información se puede utilizar para mejorar el flujo del sitio web y propiciar que los clientes adquieran productos adicionales.  
  
 Después de completar las tareas de esta lección, habrá creado un modelo de minería de datos que use el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../includes/msconame-md.md)] para predecir cuál será el siguiente artículo que los clientes incluirán en la cesta de la compra. Experimentará con dos versiones del modelo: una que analiza solo el orden de productos en la cesta y otra que contiene datos demográficos adicionales del cliente para la agrupación en clústeres. Finalmente, utilizará los modelos para crear predicciones que puede utilizar para recomendar productos a los clientes.  
  
 Para completar las tareas de la lección, utilizará la estructura de minería de datos Market Basket que creó en la [Lección 3: generar un escenario de cesta de la compra &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md). Esta lección contiene las siguientes tareas:  
  
-   [Crear una estructura de modelos de minería de datos de clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
-   [Procesar el modelo de agrupación en clústeres de secuencia](../../2014/tutorials/processing-the-sequence-clustering-model.md)  
  
-   [Explorar el modelo de agrupación en clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Crear un modelo de agrupación en clústeres de secuencia relacionado &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
-   [Crear predicciones en un modelo de agrupación en clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/create-predictions-on-model-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear una estructura de modelos de minería de datos de clústeres de secuencia &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/create-sequence-clustering-mining-model-intermediate-data-mining.md)  
  
## <a name="all-lessons"></a>Todas las lecciones  
 [Lección 1: crear la solución intermedia de minería de datos &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lección 2: generar un escenario de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 [Lección 3: Generar un escenario de cesta de la compra &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)  
  
 Lección 4: Escenario de agrupación en clústeres de secuencia (tutorial intermedio de minería de datos)  
  
 [Lección 5: Generar modelos de red neuronal y de regresión logística &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Tutorial intermedio de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  
