---
title: Elemento HoldoutMaxPercent | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4c2b6c560d497bb1f5a54e704063459505d71229
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032886"
---
# <a name="holdoutmaxpercent-element"></a>Elemento HoldoutMaxPercent
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica el porcentaje máximo de casos del origen de datos que se usará para la partición de exclusión que contiene el conjunto de pruebas de un [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) elemento. Los casos restantes se usan para aprendizaje. Un valor 0 indica que no hay ningún límite con respecto al número de casos que se pueden considerar como el conjunto de pruebas.  
  
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
|Elemento primario|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Si especifica los valores de **HoldoutMaxPercent** y **HoldoutMaxCases**, el algoritmo limita el conjunto de pruebas en el menor de los dos valores.  
  
 Si **HoldoutMaxCases** se establece en el valor predeterminado es 0, y no se ha establecido un valor para **HoldoutMaxPercent**, el algoritmo utiliza el conjunto de datos completo para el entrenamiento.  
  
 Las nuevas propiedades **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, o **HoldoutActualSize** sólo están disponibles en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] y versiones posteriores. Por lo tanto, es necesario establecer estas propiedades como prefijos usando el nuevo espacio de nombres, tal como se muestra en la descripción de la sintaxis, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
> [!NOTE]  
>  En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admitía el uso de particiones de exclusión en una estructura de minería de datos. Por lo tanto, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instrucciones de Scripting Language (ASSL) que contengan uno de los parámetros de exclusión, **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, o **HoldoutActualSize**, no se puede usar en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Si usa uno de estos parámetros de exclusión en una instrucción ASSL en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] devolverá un error.  
  
 El elemento que corresponde al elemento primario de **HoldoutMaxPercent** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](../../../analysis-services/scripting/properties/properties-assl.md)   
 [Elemento HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)   
 [Holdoutseed, elemento](../../../analysis-services/scripting/properties/holdoutseed-element.md)   
 [Elemento HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)  
  
  
