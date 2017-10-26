---
title: Elemento ActionID (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- ActionID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ActionID
helpviewer_keywords:
- ActionID element
ms.assetid: 2c9c66b2-a7ea-4874-a0ed-020ce3feab20
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7a37bba497503e9d3c01031e3256baa86d1e3e0a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="actionid-element-assl"></a>Elemento ActionID (ASSL)
  Contiene el nombre de un [acción](../../../analysis-services/scripting/objects/action-element-assl.md) elemento definido en un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento que esté disponible en un [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md) elemento como un [PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PerspectiveAction>  
   <ActionID>...</ActionID  
</PerspectiveAction>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que corresponde al elemento primario de **ActionID** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PerspectiveAction>.  
  
## <a name="see-also"></a>Vea también  
 [Actions, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/collections/actions-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

