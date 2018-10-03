---
title: Consulta de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Query Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Query element
ms.assetid: 832c3337-de6d-43b2-8f1c-75bdba76539b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46720600782cb986c0fd99ee50aa21ef729289e3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149275"
---
# <a name="query-element-assl"></a>Elemento Query (ASSL)
  Contiene el texto de la consulta a ejecutar para la notificación.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<QueryNotification>  
   <Query>...</Query>  
</QueryNotification>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[QueryNotification](../objects/querynotification-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `Query` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.QueryNotification>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ProactiveCachingQueryBinding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
