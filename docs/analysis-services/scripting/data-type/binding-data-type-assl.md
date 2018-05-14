---
title: Tipo de datos (ASSL) Binding | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14b216fbc9dffd4cbaade3fd9106e824eebb55c4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="binding-data-type-assl"></a>Tipo de datos Binding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo abstracto que representa una relación de dependencia entre dos objetos en los que los datos o metadatos de uno de los objetos dependen de los datos o metadatos de un objeto enlazado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md), [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md), [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md), [TimeAttributeBinding](../../../analysis-services/scripting/data-type/timeattributebinding-data-type-assl.md), [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md), [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|Ninguno|  
|Elementos derivados|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Binding>.  
  
 Para obtener más información sobre el enlace de datos, vea [orígenes de datos y enlaces & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Elemento de tipo Binding  
 En la siguiente tabla se enumeran los elementos de tipo **Binding**.  
  
|Elemento primario|Elemento de tipo **Binding**|Comentarios|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md) de [CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md) (de tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Tipo de la **enlace** debe ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) o [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (fuera de línea)](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Tipo de la **enlace** debe ser [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**Binding** puede ser de cualquier tipo|  
|[Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md), o [ TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) o [UserDefinedGroupBinding](../../../analysis-services/scripting/data-type/userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)|[Columna](../../../analysis-services/scripting/objects/column-element-assl.md)|Tipo de la **enlace** debe ser [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md) o [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md) (de tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Tipo de la **enlace** debe ser [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), o [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md) de [KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md) (de tipo [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md))|Tipo de la **enlace** debe ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) o [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), o [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md)|Tipo de la **enlace** debe ser [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|Tipo de la **enlace** debe ser [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Partición](../../../analysis-services/scripting/objects/partition-element-assl.md)|Tipo de la **enlace** debe ser [PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](../../../analysis-services/scripting/data-type/measuregroupdimension-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [MeasureGroupDimensionBinding](../../../analysis-services/scripting/data-type/measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md), [DataSourceViewBinding](../../../analysis-services/scripting/data-type/datasourceviewbinding-data-type-assl.md), o [DimensionBinding](../../../analysis-services/scripting/data-type/dimensionbinding-data-type-assl.md)|  
|[Partición](../../../analysis-services/scripting/objects/partition-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [ProactiveCachingBinding](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|Tipo de la **enlace** debe ser [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), [tipo de datos CubeAttributeBinding &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md), o [MeasureBinding, tipo de datos &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[SourceMeasureGroup](../../../analysis-services/scripting/objects/sourcemeasuregroup-element-assl.md)|Tipo de la **enlace** debe ser [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
