---
title: Clasificar las columnas (minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 403ab773012d9e9370959bd7094db51f9785e8d0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210345"
---
# <a name="classified-columns-data-mining"></a>Columnas clasificadas (Minería de datos)
  Cuando se define una columna clasificada, se crea una relación entre la columna actual y otra columna de la estructura de minería de datos. La columna de la estructura de minería de datos que se designa como columna clasificada contiene información sobre categorías que describe los valores de otra columna de la estructura de minería de datos.  
  
 Por ejemplo, imagine que tiene dos columnas con datos numéricos: una columna, [Compras anuales], contiene las compras totales que realiza cada cliente durante un año natural determinado, mientras que la otra columna, [Desviaciones estándar], contiene las desviaciones estándar para esos valores. En este caso, podría designar la columna [Compras anuales] como columna clasificada y el modelo podría usar esta relación en el análisis.  
  
> [!NOTE]  
>  Los algoritmos proporcionados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no admiten el uso de columnas clasificadas; esta característica se proporciona para crear algoritmos personalizados.  
  
## <a name="defining-a-classified-column"></a>Definir una columna clasificada  
 El tipo de datos de una columna clasificada debe ser `Long` o `Double`.  
  
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
 [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - minería de datos&#41;](mining-structures-analysis-services-data-mining.md)   
 [Tipos de datos &#40;minería de datos&#41;](data-types-data-mining.md)  
  
  
