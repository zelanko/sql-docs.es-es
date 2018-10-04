---
title: Elemento ServerProperties (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ServerProperties Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ServerProperties
helpviewer_keywords:
- ServerProperties element
ms.assetid: 8ccbef3f-1388-4fa3-b0a4-c89b89f09056
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95e921a9bc531b66b38423df74f33e2bb53d8078
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157485"
---
# <a name="serverproperties-element-assl"></a>Elemento ServerProperties (ASSL)
  Contiene la colección de [ServerProperty](../objects/serverproperty-element-assl.md) elementos asociados con un [Server](../objects/server-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Server>  
      ...  
   <ServerProperties>  
      <ServerProperty>...</ServerProperty>  
   </ServerProperties>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Server](../objects/server-element-assl.md)|  
|Elementos secundarios|[ServerProperty](../objects/serverproperty-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ServerPropertyCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
