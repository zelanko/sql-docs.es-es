---
title: Elemento HoldoutMaxCases | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- HoldoutMaxCases
helpviewer_keywords:
- HoldoutMaxCases element
ms.assetid: 58d94d10-e11e-4368-b3b8-dff23e1947cd
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1e49da22961d21088649b4eda4539e357998049e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="holdoutmaxcases-element"></a>Elemento HoldoutMaxCases
  Especifica el número máximo de casos del origen de datos que se usará para la partición de exclusión que contiene el conjunto de pruebas de un [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento. Los escenarios restantes en el conjunto de datos se usan para aprendizaje. Un valor 0 indica que no hay ningún límite con respecto al número de casos que se pueden considerar como el conjunto de pruebas.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructure>  
   ...  
   <ddl100_100:HoldoutMaxCases>...</ddl100_100:HoldoutMaxCases>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Entero mayor que 0.|  
|Valor predeterminado|0|  
|Cardinalidad|0-1: Elemento opcional que puede producirse una sola y única vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Si especifica los valores de **HoldoutMaxPercent** y **HoldoutMaxCases**, el algoritmo limita el conjunto de pruebas en el menor de los dos valores.  
  
 Si **HoldoutMaxCases** se establece en el valor predeterminado es 0, y no se ha establecido un valor para **HoldoutMaxPercent**, el algoritmo utiliza el conjunto de datos completo para el entrenamiento.  
  
 Las nuevas propiedades **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, o **HoldoutActualSize** sólo están disponibles en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y versiones posteriores. Por lo tanto, es necesario establecer estas propiedades como prefijos con el nuevo espacio de nombres, tal como se muestra en la descripción de la sintaxis, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
> [!NOTE]  
>  En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admitía el uso de particiones de exclusión en una estructura de minería de datos. Por lo tanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instrucciones de Scripting Language (ASSL) que contengan uno de los parámetros de exclusión, **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, o **HoldoutActualSize**, no se puede usar en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si usa uno de estos parámetros de exclusión en una instrucción ASSL en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
 El elemento que corresponde al elemento primario de **HoldoutMaxCases** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [Elemento HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)   
 [Holdoutseed, elemento](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [Elemento HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  

