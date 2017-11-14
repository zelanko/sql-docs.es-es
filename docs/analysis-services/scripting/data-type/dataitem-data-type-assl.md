---
title: Tipo de datos DataItem (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DataItem Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3986d23e02287fcf1d411df19a7b46a8768489b7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dataitem-data-type-assl"></a>Tipo de datos DataItem (ASSL)
  Define un tipo de datos primitivo que representa las características relacionadas con datos de un elemento de datos, como una columna o un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataItem>  
   <DataType>...</DataType>  
   <DataSize>...</DataSize>  
   <MimeType>...</MimeType>  
   <NullProcessing>...</NullProcessing>  
   <Trimming>...</Trimming>  
   <InvalidXmlCharacters>...</InvalidXmlCharacters>  
      <Collation>...</Collation>  
   <Format>...</Format>  
   <Source>...</Source>  
   <Annotations>...</Annotations>  
</DataItem>  
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
|Elementos secundarios|[Anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [intercalación](../../../analysis-services/scripting/properties/collation-element-assl.md), [DataSize](../../../analysis-services/scripting/properties/datasize-element-assl.md), [DataType](../../../analysis-services/scripting/properties/datatype-element-assl.md), [formato](../../../analysis-services/scripting/properties/format-element-assl.md), [InvalidXmlCharacters ](../../../analysis-services/scripting/properties/invalidxmlcharacters-element-assl.md), [MimeType](../../../analysis-services/scripting/properties/mimetype-element-assl.md), [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md), [origen](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [Trimming](../../../analysis-services/scripting/properties/trimming-element-assl.md)|  
|Elementos derivados|Vea la tabla de Notas.|  
  
## <a name="remarks"></a>Comentarios  
 El **DataItem** tipo de datos se utiliza para cualquier elemento de datos que se puede enlazar; por ejemplo, una medida, clave de atributo y el nombre del atributo. Los detalles que son pertinentes y los valores predeterminados que se aplican dependen del uso; por ejemplo, los nombres de atributo deben ser las cadenas.  
  
 Una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] acepta solo un cierto conjunto de tipos de datos. El uso de otros tipos de datos genera un error, en lugar de una conversión implícita a uno de los tipos válidos.  
  
 En la tabla siguiente enumera los elementos de tipo **DataItem**.  
  
|Elemento primario|Elemento de tipo **DataItem**|Comentarios|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../../../analysis-services/scripting/data-type/attributetranslation-data-type-assl.md)|[CaptionColumn](../../../analysis-services/scripting/objects/captioncolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) o [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupColumn](../../../analysis-services/scripting/objects/customrollupcolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) o [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[CustomRollupPropertiesColumn](../../../analysis-services/scripting/objects/customrolluppropertiescolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) o [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) o [TimeBinding](../../../analysis-services/scripting/data-type/timebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) o [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[SkippedLevelsColumn](../../../analysis-services/scripting/objects/skippedlevelscolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) o [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|[UnaryOperatorColumn](../../../analysis-services/scripting/objects/unaryoperatorcolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md) o [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)|  
|[Medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|[Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md), [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md), o [CubeDimensionBinding](../../../analysis-services/scripting/data-type/cubedimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md), [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md) o [InheritedBinding](../../../analysis-services/scripting/data-type/inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[KeyColumn](../../../analysis-services/scripting/objects/keycolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|[NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)|[ForeignKeyColumn](../../../analysis-services/scripting/objects/foreignkeycolumn-element-assl.md)|**Origen** elemento de la **DataItem** debe ser de tipo [ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

