---
title: "Las columnas del modelo de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [data mining], mining model columns
- columns [data mining]
- REGRESSOR column
- columns [data mining], modeling flags
- modeling flags [data mining]
- MODEL_EXISTENCE_ONLY column
- usage property [data mining]
ms.assetid: fab47643-5bfd-424e-a0f7-69e665db6bab
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2691f87c4ded8d2e9f00e4390681c936591bc83
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mining-model-columns"></a>Columnas del modelo de minería de datos
  Un modelo de minería de datos aplica un algoritmo de modelo de minería a los datos que se representan en una estructura de minería de datos. Al igual que la estructura, el modelo de minería de datos contiene columnas. La estructura de minería contiene el modelo de minería de datos y éste hereda todos los valores de las propiedades que define la estructura. El modelo puede utilizar todas las columnas que contiene la estructura de minería de datos o un subconjunto de las columnas.  
  
 En una columna de minería de datos puede definir dos elementos adicionales de información: uso y marcas de modelado.  
  
-   El**uso** es una propiedad que define cómo el modelo va a usar la columna. Las columnas se pueden usar como columnas de entrada, de clave o de predicción.  
  
-   Las**marcas de modelado** proporcionan al algoritmo información adicional sobre los datos que se definen en la tabla de casos, de forma que el algoritmo pueda generar un modelo más preciso. Puede definir marcas de modelado mediante programación con el lenguaje DMX (Extensiones de minería de datos) o en el **Diseñador de minería de datos** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 La siguiente lista describe las marcas de modelado que puede definir en una columna de modelo de minería de datos.  
  
 **MODEL_EXISTENCE_ONLY**  
 Indica que la presencia del atributo es más importante que los valores que están en la columna de atributos. Por ejemplo, considere una tabla de casos que contenga una lista de elementos de pedido asociados con un cliente determinado. Los datos de la tabla incluyen el tipo de producto, el Id. y el costo de cada elemento. Para el modelado, el hecho de que el cliente haya adquirido un elemento de pedido concreto podría ser más importante que el costo del propio elemento. En este caso, es necesario marcar la columna de costo como **MODEL_EXISTENCE_ONLY**.  
  
 **REGRESSOR**  
 Indica que el algoritmo puede usar la columna especificada en la fórmula de regresión de algoritmos de regresión. Esta marca se admite en los algoritmos de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] y de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Para más información sobre la configuración de la propiedad de uso y la definición de marcas de modelado mediante programación con DMX, vea [CREATE MINING MODEL &#40;DMX&#41;](../../dmx/create-mining-model-dmx.md). Para más información sobre la configuración de la propiedad de uso y la definición de marcas de modelado en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vea [Mover objetos de minería de datos](../../analysis-services/data-mining/moving-data-mining-objects.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Cambiar las propiedades de un modelo de minería de datos](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)   
 [Excluir una columna de un modelo de minería de datos](../../analysis-services/data-mining/exclude-a-column-from-a-mining-model.md)   
 [Columnas de la estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  

