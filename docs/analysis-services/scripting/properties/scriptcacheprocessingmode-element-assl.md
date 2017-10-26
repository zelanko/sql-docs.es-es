---
title: Elemento ScriptCacheProcessingMode (ASSL) | Documentos de Microsoft
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
- ScriptCacheProcessingMode Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ScriptCacheProcessingMode
helpviewer_keywords:
- ScriptCacheProcessingMode element
ms.assetid: 95c0723c-69a4-43e7-b743-f712180a7681
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1982cc5b9266f8d69d0975043c307ec3272d8149
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="scriptcacheprocessingmode-element-assl"></a>Elemento ScriptCacheProcessingMode (ASSL)
  Indica el servidor debería generar la caché de script durante o después del procesamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube>  
   ...  
      <ScriptCacheProcessingMode>...</ScriptCacheProcessingMode>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Regular*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Regular*|El servidor genera la caché de script durante el procesamiento.|  
|*Diferida*|El servidor genera la caché de script tras el procesamiento.|  
  
 La enumeración que corresponde a los valores permitidos para **ScriptCacheProcessingMode** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ScriptCacheProcessingMode>.  
  
 El elemento que corresponde al elemento primario de **ScriptCacheProcessingMode** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Cube>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

