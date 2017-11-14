---
title: Elemento ProcessingQuery (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- ProcessingQuery Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProcessingQuery element
ms.assetid: d18e6f4b-c24c-4f73-8b85-4b6e8a82a695
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f9c2d9f0607e51f754657a5cbd2750eff5fc173a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 En la tabla en la [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md) al que hace referencia el **ProcessingQuery** se identifica mediante el elemento relacionado, [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md).  
  
 El elemento que corresponde al elemento primario de **ProcessingQuery** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

