---
title: Elemento HoldoutMaxPercent | Microsoft Docs
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
- HoldoutMaxPercent
helpviewer_keywords:
- HoldoutMaxPercent element
ms.assetid: e375cc51-5f9d-4252-98a1-326ca0dbbf83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ef3a056404f350ea8b9bfe5d369b9091bad0de9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140275"
---
# <a name="holdoutmaxpercent-element"></a>Elemento HoldoutMaxPercent
  Especifica el porcentaje máximo de casos del origen de datos que se usará para la partición de exclusión que contiene el conjunto de pruebas de un [MiningStructure](../objects/miningstructure-element-assl.md) elemento. Los casos restantes se usan para aprendizaje. Un valor 0 indica que no hay ningún límite con respecto al número de casos que se pueden considerar como el conjunto de pruebas.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxPercent>...</ddl100_100:HoldoutMaxPercent>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Entero entre 0 y 99|  
|Valor predeterminado|30|  
|Cardinalidad|0-1: Elemento opcional que puede producirse una sola y única vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Si especifica los valores de `HoldoutMaxPercent` y `HoldoutMaxCases`, el algoritmo limita el conjunto de pruebas al menor de los dos valores.  
  
 Si `HoldoutMaxCases` está establecido en el valor predeterminado de 0 y no se ha establecido un valor para `HoldoutMaxPercent`, el algoritmo usa el conjunto de datos completo para aprendizaje.  
  
 Las nuevas propiedades `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed`, o `HoldoutActualSize` solo están disponibles en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y versiones posteriores. Por lo tanto, es necesario establecer estas propiedades como prefijos usando el nuevo espacio de nombres, tal como se muestra en la descripción de la sintaxis, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
> [!NOTE]  
>  En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admitía el uso de particiones de exclusión en una estructura de minería de datos. Por consiguiente, las instrucciones ASSL (Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]) que contengan uno de los parámetros de exclusión `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` o `HoldoutActualSize`, no se pueden utilizar en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si usa uno de estos parámetros de exclusión en una instrucción ASSL en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
 El elemento que se corresponde con el elemento primario de `HoldoutMaxPercent` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)   
 [Elemento HoldoutMaxCases](holdoutmaxcases-element.md)   
 [Elemento HoldoutSeed](holdoutseed-element.md)   
 [Elemento HoldoutActualSize](holdoutactualsize-element.md)  
  
  
