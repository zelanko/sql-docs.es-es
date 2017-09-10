---
title: "Clasifica columnas (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- content types [data mining]
- STDEV column
- VARIANCE column
- PROBABLILITY column
- PROBABILITY_STDEV column
- columns [data mining], classified
- classified columns [data mining]
- PROBABILITY_VARIANCE column
- SUPPORT column
ms.assetid: 68bf3b78-dc12-497c-898f-b43a45646123
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d114c3495c213e5493e3ccb87c1201d0517e4edf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="classified-columns-data-mining"></a>Columnas clasificadas (Minería de datos)
  Cuando se define una columna clasificada, se crea una relación entre la columna actual y otra columna de la estructura de minería de datos. La columna de la estructura de minería de datos que se designa como columna clasificada contiene información sobre categorías que describe los valores de otra columna de la estructura de minería de datos.  
  
 Por ejemplo, imagine que tiene dos columnas con datos numéricos: una columna, [Compras anuales], contiene las compras totales que realiza cada cliente durante un año natural determinado, mientras que la otra columna, [Desviaciones estándar], contiene las desviaciones estándar para esos valores. En este caso, podría designar la columna [Compras anuales] como columna clasificada y el modelo podría usar esta relación en el análisis.  
  
> [!NOTE]  
>  Los algoritmos proporcionados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no admiten el uso de columnas clasificadas; esta característica se proporciona para crear algoritmos personalizados.  
  
## <a name="defining-a-classified-column"></a>Definir una columna clasificada  
 El tipo de datos de una columna clasificada debe ser **Long** o **Double**.  
  
 En la lista siguiente se describen los tipos de contenido que admite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para las columnas clasificadas.  
  
 **PROBABILITY**  
 El valor de la columna es la probabilidad del valor asociado, un número entre cero y uno.  
  
 **VARIANCE**  
 El valor de la columna es la varianza del valor asociado.  
  
 **STDEV**  
 El valor de la columna es la desviación estándar del valor asociado.  
  
 **PROBABILITY_VARIANCE**  
 El valor de la columna es la varianza de la probabilidad del valor asociado.  
  
 **PROBABILITY_STDEV**  
 El valor de la columna es la desviación estándar de la probabilidad del valor asociado.  
  
 **Support**  
 El valor de la columna es el peso, o factor de replicación del caso, del valor asociado.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tipos de datos &#40;minería de datos&#41;](../../analysis-services/data-mining/data-types-data-mining.md)  
  
  
