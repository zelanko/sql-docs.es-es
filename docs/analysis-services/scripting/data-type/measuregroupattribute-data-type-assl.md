---
title: Tipo de datos MeasureGroupAttribute (ASSL) | Documentos de Microsoft
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
- MeasureGroupAttribute Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroupAttribute
helpviewer_keywords:
- MeasureGroupAttribute data type
ms.assetid: dc7f71e6-3755-4d99-9fcd-5830e10eb653
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 334722f0a765e0e1d83a5014a3882552ccf7fa2b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroupattribute-data-type-assl"></a>Tipo de datos MeasureGroupAttribute (ASSL)
  Define un tipo de datos primitivo que representa la relación entre un atributo y un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroupAttribute>  
   <AttributeID>...</AttributeID>  
      <KeyColumns>...</KeyColumns>  
   <Type>...</Type>  
   <Annotations>...</Annotations>  
</MeasureGroupAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md), [tipo](../../../analysis-services/scripting/properties/type-element-measuregroupattribute-assl.md)|  
|Elementos derivados|[Atributo](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md) colección de [RegularMeasureGroupDimension](../../../analysis-services/scripting/data-type/regularmeasuregroupdimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

