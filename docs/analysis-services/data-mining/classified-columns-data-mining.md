---
title: "Clasifica columnas (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
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
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 02792608fce3f2cca0c1bf78e5215b1a0b607a1e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="classified-columns-data-mining"></a>Columnas clasificadas (Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Cuando define una columna clasificada, se crea una relación entre la columna actual y otra columna en la estructura de minería de datos. La columna de la estructura de minería de datos que se designa como columna clasificada contiene información sobre categorías que describe los valores de otra columna de la estructura de minería de datos.  
  
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
  
  
