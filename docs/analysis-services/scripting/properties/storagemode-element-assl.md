---
title: Elemento StorageMode (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- StorageMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- StorageMode
helpviewer_keywords:
- StorageMode element
ms.assetid: 197e8153-1ab6-43ba-a7e9-ae9be19ac511
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5c166d27a9047a0cf5e5aabb9b7f1b0f21713df0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="storagemode-element-assl"></a>Elemento StorageMode (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Determina el modo de almacenamiento para el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, Partition -->  
   ...  
   <StorageMode>...</StorageMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*MOLAP*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CUBE, elemento &#40; ASSL &#41; ](../../../analysis-services/scripting/objects/cube-element-assl.md), [Dimensión elemento &#40; ASSL &#41; ](../../../analysis-services/scripting/objects/dimension-element-assl.md), [MeasureGroup, elemento &#40; ASSL &#41; ](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [Partición elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*MOLAP*|El elemento primario usa el almacenamiento OLAP multidimensional (MOLAP).|  
|*ROLAP*|El elemento primario usa el almacenamiento OLAP relacional (ROLAP).|  
|*HOLAP*|El elemento primario usa el almacenamiento OLAP híbrido (HOLAP).<br /><br /> Nota: Este valor no es válido para [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md) elementos primarios.|  
|*InMemory*|El elemento primario utiliza el almacenamiento IMBI.|  
  
 La enumeración que corresponde a los valores permitidos para **StorageMode** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.StorageMode>.  
  
 Los elementos que corresponden a los elementos primarios de **StorageMode** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MeasureGroup>, y <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
