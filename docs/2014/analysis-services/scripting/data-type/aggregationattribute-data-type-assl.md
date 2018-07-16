---
title: Tipo de datos AggregationAttribute (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AggregationAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationAttribute
helpviewer_keywords:
- AggregationAttribute data type
ms.assetid: 636827c7-938d-4b7d-9827-46da3bc60d9a
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 71da4468ab4edece07744ae73a13243eefd1dfed
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243425"
---
# <a name="aggregationattribute-data-type-assl"></a>Tipo de datos AggregationAttribute (ASSL)
  Define un tipo de datos primitivo que representa la asociación entre un [agregación](../objects/aggregation-element-assl.md) elemento y un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AggregationAttribute>  
   <AttributeID>...</AttributeID>  
      <Annotations>...</Annotations>  
</AggregationAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[AttributeID](../properties/id-element-assl.md), [anotaciones](../collections/annotations-element-assl.md)|  
|Elementos derivados|[Atributo](../objects/attribute-element-assl.md) ([atributos](../collections/attributes-element-assl.md) colección de [AggregationDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Notas  
 La clase correspondiente en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.AggregationAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento aggregation &#40;ASSL&#41;](../objects/aggregation-element-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
