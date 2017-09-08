---
title: Elemento DiscretizationBucketCount (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DiscretizationBucketCount Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DiscretizationBucketCount
helpviewer_keywords:
- DiscretizationBucketCount element
ms.assetid: 551a73ae-59e1-4079-a2d9-988df96b5e07
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80e3dcaa9c2cd5ee79dd1873c85b23d0a8054b33
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discretizationbucketcount-element-assl"></a>Elemento DiscretizationBucketCount (ASSL)
  Contiene el número de depósitos en los que discretizar.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute> <!-- or ScalarMiningStructureColumn -->  
   ...  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Integer|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **DiscretizationBucketCount** elemento determina cuántos grupos o "cubos" se crean cuando los valores para la **DimensionAttribute** o **ScalarMiningStructureColumn**  se discretizado o se organizan en un conjunto específico de grupos. Si no se especifica el elemento, o si se especifica cero como el valor del elemento, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un número adecuado de grupos en función del método de discretización. Para obtener más información acerca de los métodos de discretización, vea [métodos de discretización &#40; minería de datos &#41;](../../../analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Los elementos que corresponden a los elementos primarios de **DiscretizationBucketCount** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.DimensionAttribute> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [DiscretizationMethod, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
