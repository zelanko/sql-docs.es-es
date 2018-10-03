---
title: Elemento DataAggregation (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataAggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataAggregation element
ms.assetid: baf6d2c9-54f6-4a6d-95f7-e1e758be458d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01a86977cc6ebf85d004bf235b6d47a354e112a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134825"
---
# <a name="dataaggregation-element-assl"></a>Elemento DataAggregation (ASSL)
  Determina si la instancia puede agregar datos persistentes o datos almacenados en caché para el [MeasureGroup](../objects/group-element-assl.md).  
  
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
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MeasureGroup](../objects/group-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Ninguno*|La agregación no se lleva a cabo para este grupo de medida.|  
|*DataAggregatable*|Los datos almacenados se pueden agregar para este grupo de medida.|  
|*CacheAggregatable*|Los datos almacenados en caché se pueden agregar para este grupo de medida.|  
|*DataAndCacheAggregatable*|Tanto los datos almacenados como los datos almacenados en caché se pueden agregar para este grupo de medida.|  
  
 El elemento que se corresponde con el elemento primario de `DataAggregation` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento de dimensión &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
