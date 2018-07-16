---
title: Tipo de datos MeasureGroupDimension (ASSL) | Microsoft Docs
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
- MeasureGroupDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroupDimension
helpviewer_keywords:
- MeasureGroupDimension data type
ms.assetid: 9d1c1c19-31ce-4c42-b2e6-4c1b08875a83
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcbba7071e1f2efc8ede59259a48a334652de81
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249125"
---
# <a name="measuregroupdimension-data-type-assl"></a>Tipo de datos MeasureGroupDimension (ASSL)
  Define un tipo de datos primitivo abstracto que representa la relación existente entre una dimensión y un grupo de medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroupDimension>  
   <CubeDimensionID>...</CubeDimensionID>  
      <Annotations>...</Annotations>  
   <Source>...</Source>  
</MeasureGroupDimension>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[DataMiningMeasureGroupDimension](dimension-data-type-assl.md), [DegenerateMeasureGroupDimension](measuregroupdimension-data-type-assl.md), [ManyToManyMeasureGroupDimension](manytomanymeasuregroupdimension-data-type-assl.md), [ReferenceMeasureGroupDimension](referencemeasuregroupdimension-data-type-assl.md), [RegularMeasureGroupDimension](regularmeasuregroupdimension-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Annotations](../collections/annotations-element-assl.md), [CubeDimensionID](../properties/id-element-assl.md), [Source](../properties/source-element-binding-assl.md)|  
|Elementos derivados|[Dimension](../objects/dimension-element-assl.md) ([colección Dimensions](../collections/dimensions-element-assl.md) de [MeasureGroup](../objects/group-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 Cada `MeasureGroupDimension` es una referencia a una de las dimensiones del cubo. Éstos definen qué dimensiones de cubo se aplican al grupo de medida.  
  
 El conjunto de atributos que se proporcionan determina la granularidad (ámbito) en la que se conocen las medidas del grupo de medida. Por ejemplo, las medidas que representan las ventas de productos están contenidas en el grupo de medida Sales. La información de estas medidas se almacena en el origen de datos subyacente con una granularidad mensual, en vez de semanal o diaria. En este caso, solo debería aparecer listado el atributo Month para el `MeasureGroupDimension` que describe la relación existente entre una dimensión de tiempo y el grupo de medida Sales. En algún caso aislado, la granularidad se podría definir en términos de un conjunto de atributos. Por ejemplo, dado el conjunto de atributos {Day, Week, Month, Year}, donde Day implica Week y Month, pero Week no implica Month, podrían conocerse las medidas contenidas en el grupo de medida Forecasts por Month y Week, pero no por Day.  
  
 Si no se proporciona ningún atributo, es como si solo apareciera en la lista el atributo clave de la dimensión (que define el nivel mínimo de granularidad). Cada partición de un grupo de medida debe tener la misma granularidad. El conjunto de atributos enumerado no debería ser redundante con respecto a las relaciones entre atributos. Por ejemplo, si Month implica Year, la granularidad se define como Month, no como Month y Year.  
  
 Un `MeasureGroupDimension` necesita incluir una jerarquía solo si tiene algo específico que así lo indique. (No hay ninguna manera de seleccionar qué jerarquías se aplican a un grupo de medida determinado). De igual forma, necesita incluir un [MeasureGroupAttribute](measuregroupattribute-data-type-assl.md) solo si tiene algo específico que así lo indique.  
  
 Cada jerarquía debe ser un subconjunto de las jerarquías incluidas en [CubeDimension](cubedimension-data-type-assl.md). No es posible seleccionar los niveles, aunque algunos se podrían deshabilitar automáticamente dependiendo de la granularidad del grupo de medida.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
