---
title: Habilita el elemento (ASSL) | Documentos de Microsoft
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
apiname:
- Enabled Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Enabled
helpviewer_keywords:
- Enabled element
ms.assetid: dbe57903-75c0-4060-a2b3-eab241d7469f
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8832c5d6ec6dcba3c49289ada700572b657f821c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="enabled-element-assl"></a>Elemento Enabled (ASSL)
  Indica si el elemento primario está habilitado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeHierarchy> <!-- or ProactiveCaching -->  
   ...  
   <Enabled>...</Enabled>  
   ...  
</CubeHierarchy>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Booleano|  
|Valor predeterminado|True|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Los elementos que corresponden a los elementos primarios de **habilitado** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.CubeHierarchy> y <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

