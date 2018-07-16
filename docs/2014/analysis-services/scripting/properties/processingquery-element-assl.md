---
title: Elemento ProcessingQuery (ASSL) | Microsoft Docs
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
- ProcessingQuery Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ProcessingQuery element
ms.assetid: d18e6f4b-c24c-4f73-8b85-4b6e8a82a695
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01d9ccc0e5e5c376e0d5e7ee08aa42eb0e062b97
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250895"
---
# <a name="processingquery-element-assl"></a>Elemento ProcessingQuery (ASSL)
  Contiene el texto parametrizado de la consulta que se debe ejecutar para la notificación del estado de procesamiento incremental.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<IncrementalProcessingNotification>  
   ...  
   <ProcessingQuery>...</ProcessingQuery>  
   ...  
</IncrementalProcessingNotification>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 La tabla en la [DataSourceView](../objects/datasourceview-element-assl.md) que hace referencia el `ProcessingQuery` se identifica mediante el elemento relacionado, [TableID](id-element-assl.md).  
  
 El elemento que se corresponde con el elemento primario de `ProcessingQuery` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
