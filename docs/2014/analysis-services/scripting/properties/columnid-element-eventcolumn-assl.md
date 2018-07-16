---
title: Elemento ColumnID (EventColumn) (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ColumnID Element (EventColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ColumnID
helpviewer_keywords:
- ColumnID element
ms.assetid: c4f4fbad-9d70-4de2-8cf7-caee80a4a1e4
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82cc6d67aa0c1533b9779b93468fdf8845272cde
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245605"
---
# <a name="columnid-element-eventcolumn-assl"></a>Elemento ColumnID (EventColumn) (ASSL)
  Contiene el identificador (ID) de la columna de información que va a capturar para un evento como parte de un [seguimiento](../objects/trace-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<EventColumn>  
   <ColumnID>...</ColumnID>  
</EventColumn>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[EventColumn](../data-type/eventcolumn-data-type-assl.md)|  
|Elementos secundarios|Ninguno.|  
  
## <a name="remarks"></a>Notas  
 El elemento que se corresponde con el elemento primario de `ColumnID` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.TraceColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Columns &#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Elemento de evento &#40;ASSL&#41;](../objects/event-element-assl.md)   
 [Elemento Events &#40;ASSL&#41;](../collections/events-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
