---
title: Origen de elemento (Binding) (ASSL) | Documentos de Microsoft
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
- Source Element (Binding)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 1032558c-7546-4ca7-888d-8139df23cb62
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 58bacab7c84d1432a57d16c709b08c8c79ac143d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200430"
---
# <a name="source-element-binding-assl"></a>Elemento Source (Binding) (ASSL)
  Identifica el origen de datos al que está enlazado el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AggregationInstance> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Source>...</Source>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Tabla de tipos de datos; Vea a continuación|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
 **Tipo de datos y longitud**  
  
|||  
|-|-|  
|Antecesor o elemento primario|Tipo de datos|  
|[AggregationInstance](../data-type/binding-data-type-assl.md)|  
|[AggregationInstanceMeasure](../data-type/columnbinding-data-type-assl.md)|  
|[Cubo](../data-type/datasourceviewbinding-data-type-assl.md)|  
|[Elemento de datos](../data-type/dataitem-data-type-assl.md)|Cualquier tipo de datos derivado de [enlace](../data-type/binding-data-type-assl.md), en función del elemento primario de `DataItem`. Para obtener más información, vea la sección Comentarios.|  
|[Dimensión](../data-type/dimensionbinding-data-type-assl.md), [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md), [TimeBinding](../data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md), [UserDefinedGroupBinding](../data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[MeasureGroup](../data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupDimension](../data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[CubeDimensionBinding](../data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../data-type/dimensionbinding-data-type-assl.md)|  
|[Partición](../data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|Cualquier tipo de datos derivado de [ProactiveCachingBinding](../data-type/proactivecachingbinding-data-type-assl.md), en función de las opciones de notificación y procesamiento usadas por el elemento primario de la `ProactiveCaching` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AggregationInstance](../objects/aggregationinstance-element-assl.md), [AggregationInstanceMeasure](../data-type/aggregationinstancemeasure-data-type-assl.md), [cubo](../objects/cube-element-assl.md), [DataItem](../data-type/dataitem-data-type-assl.md), [dimensión](../objects/dimension-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [MeasureGroup](../objects/group-element-assl.md), [MeasureGroupDimension](../data-type/dimension-data-type-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [partición ](../objects/partition-element-assl.md), [ProactiveCaching](../objects/proactivecaching-element-assl.md).|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 En el elemento `Source`, los tipos de datos `Binding` derivados permitidos en el elemento `DataItem` dependen del elemento primario del elemento `DataItem`.  
  
|Elemento primario DataItem|Tipos de datos admitidos|  
|---------------------|------------------------|  
|[DimensionAttribute](../data-type/attributebinding-data-type-assl.md), [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [TimeAttributeBinding](../data-type/timeattributebinding-data-type-assl.md) (sólo para [KeyColumns](../collections/columns-element-assl.md)).|  
|[MeasureGroupAttribute](../data-type/measuregroupattribute-data-type-assl.md)|[AttributeBinding](../data-type/attributebinding-data-type-assl.md), [ColumnBinding](../data-type/columnbinding-data-type-assl.md), [InheritedBinding](../data-type/inheritedbinding-data-type-assl.md).|  
|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|[ColumnBinding](../data-type/columnbinding-data-type-assl.md)|  
  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, consulte [tipo de datos de enlace &#40;ASSL &#41;](../data-type/binding-data-type-assl.md).  
  
 Para obtener más información sobre los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;SSAS multidimensionales&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  