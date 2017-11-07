---
title: Elemento DataAggregation (ASSL) | Documentos de Microsoft
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
- DataAggregation Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataAggregation element
ms.assetid: baf6d2c9-54f6-4a6d-95f7-e1e758be458d
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92556b6af8a3d56f647fcbea8b34e197fb8ce663
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dataaggregation-element-assl"></a>Elemento DataAggregation (ASSL)
  Determina si la instancia puede agregar datos persistentes o datos almacenados en caché para el [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroup>  
   ...  
   <DataAggregation>...</DataAggregation>  
   ...  
</MeasureGroup>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*DataAndCacheAggregatable*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Ninguno*|La agregación no se lleva a cabo para este grupo de medida.|  
|*DataAggregatable*|Los datos almacenados se pueden agregar para este grupo de medida.|  
|*CacheAggregatable*|Los datos almacenados en caché se pueden agregar para este grupo de medida.|  
|*DataAndCacheAggregatable*|Tanto los datos almacenados como los datos almacenados en caché se pueden agregar para este grupo de medida.|  
  
 El elemento que corresponde al elemento primario de **DataAggregation** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Vea también  
 [CUBE, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

