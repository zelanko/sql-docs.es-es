---
title: Tipo de datos RegularMeasureGroupDimension (ASSL) | Documentos de Microsoft
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
- RegularMeasureGroupDimension Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RegularMeasureGroupDimension
helpviewer_keywords:
- RegularMeasureGroupDimension data type
ms.assetid: 5c4ce400-6d7c-40fc-9bcb-392718b77182
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3cddeb31e37a4c9f1877df58a81ef4985398b487
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="regularmeasuregroupdimension-data-type-assl"></a>Tipo de datos RegularMeasureGroupDimension (ASSL)
  Define un tipo de datos derivado que representa una relación normal entre una dimensión y un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RegularMeasureGroupDimension>  
   <!-- The following elements extend MeasureGroupDimension -->  
   <Cardinality>...</Cardinality>  
   <Attributes>...</Attributes>  
</RegularMeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|  
|Tipos de datos derivados|[ReferenceMeasureGroupDimension](../../../analysis-services/scripting/data-type/referencemeasuregroupdimension-data-type-assl.md), [DegenerateMeasureGroupDimension](../../../analysis-services/scripting/data-type/degeneratemeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md), [cardinalidad](../../../analysis-services/scripting/properties/cardinality-element-assl.md)|  
|Elementos derivados|[Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([dimensiones](../../../analysis-services/scripting/collections/dimensions-element-assl.md) colección)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RegularMeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

