---
title: 'Lección 3: Creación de un escenario de Market Basket (Tutorial de minería de datos intermedios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], tutorials
- association algorithms [Analysis Services]
- nested tables
- tutorials [Data Mining]
ms.assetid: 651eef38-772e-4d97-af51-075b1b27fc5a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c2f1c5a8ae897284f07c3fd6c65d9735099a41fa
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041406"
---
# <a name="lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial"></a>Lección 3: Creación de un escenario de Market Basket (Tutorial de minería de datos intermedios)
  El departamento de marketing de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] desea mejorar el sitio web de la empresa para promover las ventas cruzadas. Como parte de la actualización del sitio, desean contar con la capacidad de predecir los productos cuya adquisición podría interesar a los clientes, basándose en otros productos que ya se encuentran en sus cestas de la compra en línea. El departamento de marketing también desea comprender mejor el comportamiento de compra de los clientes, de forma que puedan diseñar el sitio web para que los elementos que tienden a comprarse juntos aparezcan agrupados. Han aprendido que la minería de datos resulta especialmente útil para este tipo de *análisis de la cesta de la compra* y le han solicitado el desarrollo de un modelo de minería de datos.  
  
 Después de completar las tareas de esta lección, tendrá un modelo de minería de datos que muestra los grupos de elementos de las transacciones históricas del cliente. Además, puede utilizar el modelo de minería de datos para predecir elementos adicionales que un cliente puede desear comprar.  
  
 Para completar las tareas en esta lección, utilizará el origen de datos y la solución que creó en la primera lección de la [Tutorial intermedio de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md). Modificará esta solución agregando una vista del origen de datos que contiene tablas sobre el cliente, incluso una tabla anidada de sus compras.  A continuación, generará un modelo de minería de datos que utiliza el algoritmo de reglas de asociación de Microsoft, que es adecuado en escenarios de cesta de la compra.  
  
 En esta lección se incluyen los temas siguientes:  
  
-   [Agregar datos de una vista con tablas anidadas del origen &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
-   [Creación de un modelo y estructura Market Basket &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-market-basket-structure-and-model-intermediate-data-mining-tutorial.md)  
  
-   [Modificar y procesar el modelo de cesta &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/modify-process-market-basket-model-intermediate-data-mining-tutorial.md)  
  
-   [Explorar los modelos Market Basket &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
-   [Filtrar una tabla anidada en un modelo de minería de datos &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
-   [Predecir asociaciones &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Agregar datos de una vista con tablas anidadas del origen &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/adding-a-data-source-view-with-nested-tables-intermediate-data-mining-tutorial.md)  
  
## <a name="all-lessons"></a>Todas las lecciones  
 [Lección 1: Creación de la solución de minería de datos intermedios &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-1-create-solution-intermediate-data-mining-tutorial.md)  
  
 [Lección 2: Generar un escenario de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
 Lección 3: Escenario de Market Basket (Tutorial de minería de datos intermedios)  
  
 [Lección 4: Creación de una escenario de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
 [Lección 5: Creación de modelos de regresión logística y Red neuronal &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Lección 2: Generar un escenario de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)   
 [Lección 4: Creación de una escenario de clústeres de secuencia &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)  
  
  
