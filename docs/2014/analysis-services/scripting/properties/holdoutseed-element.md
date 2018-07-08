---
title: Elemento HoldoutSeed | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutSeed
helpviewer_keywords:
- HoldoutSeed element
ms.assetid: 6b608bb3-c075-4744-9722-f5fb9fa1cc7e
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b5ba2d0d5d3cb355a4d0d6a372b41207ddce1d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185232"
---
# <a name="holdoutseed-element"></a>Elemento HoldoutSeed
  Especifica el valor de inicialización para una partición de extracción repetible que contiene el conjunto de pruebas de un [MiningStructure](../objects/miningstructure-element-assl.md) elemento. Esta semilla asegura que el contenido del modelo permanece igual durante el nuevo procesamiento. Si no se especifica o se establece en 0, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea una semilla usando un algoritmo hash en el nombre de la estructura de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutSeed>...</ddl100_100:HoldoutSeed>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Long|  
|Valor predeterminado|0|  
|Cardinalidad|0-1: Elemento opcional que puede producirse una sola y única vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Al crear primero una estructura de minería de datos, el identificador y el nombre son los mismos. Sin embargo, puede cambiar el nombre de la estructura de minería de datos. Por consiguiente, si desea asegurarse de que la partición es repetible, no debería confiar en la semilla creada por el nombre sino que debería definir explícitamente una semilla.  
  
 Además, cuando crea una copia de una estructura de minería de datos mediante el `EXPORT` instrucción [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] conservará el nombre de la nueva estructura de minería de datos pero generará automáticamente un nuevo identificador. Por consiguiente, es posible tener dos estructuras de minería de datos que comparten el mismo nombre pero tienen identificadores diferentes. Dos estructuras de minería de datos que tengan el mismo nombre tendrán la misma semilla. Sin embargo, como el particionamiento de los datos también depende de los datos de origen, el contenido real de las particiones de cada estructura puede ser diferente.  
  
 Las nuevas propiedades `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, o `HoldoutActualSize` solo están disponibles en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y versiones posteriores. Por lo tanto, es necesario establecer estas propiedades como prefijos con el nuevo espacio de nombres, tal como se muestra en la descripción de la sintaxis, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
 **Tenga en cuenta** en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admitía el uso de particiones de exclusión en una estructura de minería de datos. Por lo tanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instrucciones de Scripting Language (ASSL) que contienen los parámetros de exclusión `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, o `HoldoutActualSize` no se puede usar en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si usa uno de estos parámetros de exclusión en una instrucción ASSL en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
 El elemento que se corresponde con el elemento primario de `HoldoutSeed` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutActualSize](holdoutactualsize-element.md)   
 [Elemento HoldoutMaxPercent](holdoutmaxpercent-element.md)   
 [Elemento HoldoutMaxCases](holdoutmaxcases-element.md)  
  
  
