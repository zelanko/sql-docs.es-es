---
title: Elemento NotificationTechnique (ASSL) | Documentos de Microsoft
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
- NotificationTechnique Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- NotificationTechnique element
ms.assetid: 80c43de3-f147-4bf5-bb85-da9d182ce415
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a5fdcfc7dc7d86e9036ed075e5c5332e76dc3be
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="notificationtechnique-element-assl"></a>Elemento NotificationTechnique (ASSL)
  Especifica si [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o una aplicación cliente externa procesará las notificaciones.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProactiveCachingBinding>  
   <NotificationTechnique>...</NotificationTechnique>  
</ProactiveCachingBinding>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Cliente*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Cliente*|La aplicación cliente externa procesa la notificación.|  
|*Server*|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procesa la notificación.|  
  
 El elemento que corresponde al elemento primario de **NotificationTechnique** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCachingBinding>.  
  
 La enumeración que corresponde a los valores permitidos para **NotificationTechnique** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.NotificationTechnique>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ProactiveCachingBinding &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)  
  
  

