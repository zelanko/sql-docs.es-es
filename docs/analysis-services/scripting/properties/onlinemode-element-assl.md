---
title: Elemento OnlineMode (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- OnlineMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- OnlineMode
helpviewer_keywords:
- OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf7b07efcfdc165ed3abd737aaecd241a225a71b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="onlinemode-element-assl"></a>Elemento OnlineMode (ASSL)
  Especifica si la base de datos se devuelve inmediatamente en línea cuando se inicia la nueva generación de la memoria caché o solo cuando esta se haya completado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <OnlineMode>...</OnlineMode>  
   ...  
</ProactiveCaching>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Inmediata*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Inmediata*|La base de datos se devuelve inmediatamente en línea cuando se inicia la regeneración de la caché.|  
|*OnCacheComplete*|La base de datos solo se devuelve en línea cuando se completa la regeneración de la caché.|  
  
 La enumeración que corresponde a los valores permitidos para **OnlineMode** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Vea también  
 [ProactiveCaching, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
  

