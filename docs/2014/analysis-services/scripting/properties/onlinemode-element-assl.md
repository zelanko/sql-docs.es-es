---
title: Elemento OnlineMode (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OnlineMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- OnlineMode
helpviewer_keywords:
- OnlineMode element
ms.assetid: 0bbac4e2-002f-4be4-8dd6-ccd7034f5f93
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7a4469a522b1364df645fc1dcb0362647397a89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196845"
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
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Inmediata*|La base de datos se devuelve inmediatamente en línea cuando se inicia la regeneración de la caché.|  
|*OnCacheComplete*|La base de datos solo se devuelve en línea cuando se completa la regeneración de la caché.|  
  
 La enumeración que corresponde a los valores permitidos para `OnlineMode` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento ProactiveCaching &#40;ASSL&#41;](../objects/proactivecaching-element-assl.md)  
  
  
