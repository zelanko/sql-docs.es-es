---
title: Tipo de datos (ASSL) Binding | Microsoft Docs
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
- Binding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- BINDING
helpviewer_keywords:
- Binding data type
ms.assetid: 0a777219-b885-4961-ac66-b76faeb520db
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a34209ea08d1cdfd0100bd5e2402edc0f592f066
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169546"
---
# <a name="binding-data-type-assl"></a>Tipo de datos Binding (ASSL)
  Define un tipo de datos primitivo abstracto que representa una relación de dependencia entre dos objetos en los que los datos o metadatos de uno de los objetos dependen de los datos o metadatos de un objeto enlazado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Binding>...</Binding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[AttributeBinding](binding-data-type-assl.md), [ColumnBinding](columnbinding-data-type-assl.md), [CubeAttributeBinding](cubeattributebinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), [InheritedBinding](inheritedbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), [MeasureGroupBinding](measuregroupbinding-data-type-assl.md), [ MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md), [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md), [RowBinding](rowbinding-data-type-assl.md), [TabularBinding](tabularbinding-data-type-assl.md), [ TimeAttributeBinding](timeattributebinding-data-type-assl.md), [TimeBinding](timebinding-data-type-assl.md), [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|None|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Binding>.  
  
 Para obtener más información sobre el enlace de datos, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
## <a name="elements-of-type-binding"></a>Elemento de tipo Binding  
 En la siguiente tabla se enumeran los elementos de tipo `Binding`.  
  
|Elemento primario|Elemento de tipo `Binding`|Comentarios|  
|--------------------|---------------------------------|--------------|  
|[AttributeTranslation](../properties/source-element-binding-assl.md) de [CaptionColumn](../objects/column-element-assl.md) (de tipo [DataItem](dataitem-data-type-assl.md))|Tipo de la `Binding` debe ser [AttributeBinding](binding-data-type-assl.md) o [ColumnBinding](columnbinding-data-type-assl.md)|  
|[Cubo](../objects/cube-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md)|  
|[CubeBinding (fuera de línea)](../objects/group-element-assl.md)|Tipo de la `Binding` debe ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[DataItem](dataitem-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|`Binding` puede ser de cualquier tipo|  
|[Dimension](../objects/dimension-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), [DimensionBinding](dimensionbinding-data-type-assl.md), o [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](dimensionattribute-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [AttributeBinding](binding-data-type-assl.md) o [UserDefinedGroupBinding](userdefinedgroupbinding-data-type-assl.md)|  
|[DrillThroughAction](action-data-type-assl.md)|[Columna](../objects/column-element-assl.md)|Tipo de la `Binding` debe ser [CubeAttributeBinding](cubeattributebinding-data-type-assl.md) o [MeasureBinding](measurebinding-data-type-assl.md)|  
|[Medida](../objects/measure-element-assl.md)|[Origen](../properties/source-element-binding-assl.md) (de tipo [DataItem](dataitem-data-type-assl.md))|Tipo de la `Binding` debe ser [ColumnBinding](columnbinding-data-type-assl.md), [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), o [RowBinding](rowbinding-data-type-assl.md)|  
|[MeasureGroup](../objects/measuregroup-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[Origen](../properties/source-element-binding-assl.md) de [KeyColumn](../objects/keycolumn-element-assl.md) (de tipo [DataItem](dataitem-data-type-assl.md))|Tipo de la `Binding` debe ser [AttributeBinding](binding-data-type-assl.md) o [ColumnBinding](columnbinding-data-type-assl.md), o [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](measuregroupbinding-data-type-out-of-line-assl.md)|[Dimension](../objects/dimension-element-assl.md)|Tipo de la `Binding` debe ser [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](measuregroupbinding-data-type-out-of-line-assl.md)|[Medida](../objects/measure-element-assl.md)|Tipo de la `Binding` debe ser [MeasureBinding](measurebinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](../objects/partition-element-assl.md)|Tipo de la `Binding` debe ser [PartitionBinding](partitionbinding-data-type-assl.md)|  
|[MeasureGroupBinding (fuera de línea)](measuregroupbinding-data-type-out-of-line-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [TableBinding](tablebinding-data-type-assl.md)|  
|[MeasureGroupDimension](dimension-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [MeasureGroupDimensionBinding](measuregroupdimensionbinding-data-type-assl.md)|  
|[MiningStructure](../objects/miningstructure-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [CubeDimensionBinding](dimensionbinding-data-type-assl.md), [DataSourceViewBinding](datasourceviewbinding-data-type-assl.md), o [DimensionBinding](dimensionbinding-data-type-assl.md)|  
|[Partición](../objects/partition-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [TabularBinding](tabularbinding-data-type-assl.md)|  
|[ProactiveCaching](../objects/proactivecaching-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [ProactiveCachingBinding](proactivecachingbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[Source](../properties/source-element-binding-assl.md)|Tipo de la `Binding` debe ser [AttributeBinding](binding-data-type-assl.md), [tipo de datos CubeAttributeBinding &#40;ASSL&#41;](cubeattributebinding-data-type-assl.md), o [tipo de datos MeasureBinding &#40;ASSL&#41;](measurebinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/sourcemeasuregroup-element-assl.md)|Tipo de la `Binding` debe ser [MeasureGroupBinding](measuregroupbinding-data-type-assl.md)|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
