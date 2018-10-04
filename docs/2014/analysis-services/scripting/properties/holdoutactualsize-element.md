---
title: Elemento HoldoutActualSize | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
f1_keywords:
- HoldoutActualSize
helpviewer_keywords:
- HoldoutActualSize element
ms.assetid: 606a6674-cedb-4cee-82d0-26589f084dd9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8610024c3eb0b3460883fc5eeddb80f057aff86b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096415"
---
# <a name="holdoutactualsize-element"></a>Elemento HoldoutActualSize
  Indica el tamaño real, después del procesamiento de la partición de exclusión que contiene el conjunto de pruebas de un [MiningStructure](../objects/miningstructure-element-assl.md) elemento. Los escenarios restantes en el conjunto de datos se usan para aprendizaje. Esta propiedad es de solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutActualSize>...</ddl100_100:HoldoutActualSize>  
   ...  
</MiningStructure  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Valor entero de solo lectura|  
|Valor predeterminado|No aplicable|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de `HoldoutActualSize` depende de los datos de origen y de los valores de [HoldoutMaxCases](holdoutmaxcases-element.md), [HoldoutMaxPercent](holdoutmaxpercent-element.md), y [HoldoutSeed](holdoutseed-element.md). Por consiguiente, el valor para `HoldoutActualSize` no estará disponible hasta que [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procese la estructura de minería de datos.  
  
 El elemento que se corresponde con el elemento primario de `HoldoutActualSize` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
> [!NOTE]  
>  En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admitía el uso de particiones de exclusión en una estructura de minería de datos. Por consiguiente, las instrucciones ASSL (Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]) que contengan uno de los parámetros de exclusión `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` o `HoldoutActualSize`, no se pueden utilizar en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si usa uno de estos parámetros de exclusión en una instrucción ASSL en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutMaxCases](holdoutmaxcases-element.md)   
 [Elemento HoldoutMaxPercent](holdoutmaxpercent-element.md)   
 [Elemento HoldoutSeed](holdoutseed-element.md)  
  
  
