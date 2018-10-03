---
title: Tipo de datos RegularMeasureGroupDimension (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RegularMeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RegularMeasureGroupDimension
helpviewer_keywords:
- RegularMeasureGroupDimension data type
ms.assetid: 5c4ce400-6d7c-40fc-9bcb-392718b77182
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 072ada60b803f4c8adfde73a228144a4d0157dff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051823"
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
|Tipos de datos base|[MeasureGroupDimension](dimension-data-type-assl.md)|  
|Tipos de datos derivados|[ReferenceMeasureGroupDimension](measuregroupdimension-data-type-assl.md), [DegenerateMeasureGroupDimension](degeneratemeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Atributos](../collections/attributes-element-assl.md), [cardinalidad](../properties/cardinality-element-assl.md)|  
|Elementos derivados|[Dimensión](../objects/dimension-element-assl.md) ([dimensiones](../collections/dimensions-element-assl.md) colección)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.RegularMeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
