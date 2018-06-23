---
title: Tipo de datos DataItem (ASSL) | Documentos de Microsoft
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
- DataItem Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataItem
helpviewer_keywords:
- DataItem data type
ms.assetid: f4f5155f-9c3d-49a1-a390-a9c734fafbce
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0d5622ca2cdda5a08bdcfdfd486e44b6fcd8fbf7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105948"
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
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Anotaciones](../collections/annotations-element-assl.md), [intercalación](../properties/collation-element-assl.md), [DataSize](../properties/datasize-element-assl.md), [DataType](../properties/datatype-element-assl.md), [formato](../properties/format-element-assl.md), [InvalidXmlCharacters ](../properties/invalidxmlcharacters-element-assl.md), [MimeType](../properties/mimetype-element-assl.md), [NullProcessing](../properties/nullprocessing-element-assl.md), [origen](../properties/source-element-binding-assl.md), [Trimming](../properties/trimming-element-assl.md)|  
|Elementos derivados|Vea la tabla de Notas.|  
  
## <a name="remarks"></a>Notas  
 El tipo de datos `DataItem` se utiliza para cualquier elemento de datos que se puede enlazar; por ejemplo, una medida, una clave de atributo y un nombre de atributo. Los detalles que son pertinentes y los valores predeterminados que se aplican dependen del uso; por ejemplo, los nombres de atributo deben ser las cadenas.  
  
 Una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] acepta solo un cierto conjunto de tipos de datos. El uso de otros tipos de datos genera un error, en lugar de una conversión implícita a uno de los tipos válidos.  
  
 En la siguiente tabla se enumeran los elementos de tipo `DataItem`.  
  
|Elemento primario|Elemento de tipo `DataItem`|Comentarios|  
|--------------------|----------------------------------|--------------|  
|[AttributeTranslation](../objects/column-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md) o [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrollupcolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md) o [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/customrolluppropertiescolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md) o [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/keycolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md), [AttributeBinding](attributebinding-data-type-assl.md) o [TimeBinding](timebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/namecolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md) o [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/skippedlevelscolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md) o [AttributeBinding](attributebinding-data-type-assl.md)|  
|[DimensionAttribute](../objects/unaryoperatorcolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md) o [AttributeBinding](attributebinding-data-type-assl.md)|  
|[Medida](../objects/measure-element-assl.md)|[Source](../properties/source-element-binding-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [RowBinding](rowbinding-data-type-assl.md), [ColumnBinding](binding-data-type-assl.md), [MeasureBinding](measurebinding-data-type-assl.md), o [CubeDimensionBinding](dimensionbinding-data-type-assl.md)|  
|[MeasureGroupAttribute](measuregroupattribute-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md), [AttributeBinding](attributebinding-data-type-assl.md) o [InheritedBinding](inheritedbinding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[KeyColumn](../objects/keycolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md)|  
|[ScalarMiningStructureColumn](miningstructurecolumn-data-type-assl.md)|[NameColumn](../objects/namecolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md)|  
|[TableMiningStructureColumn](../objects/foreignkeycolumn-element-assl.md)|`Source` elemento de la `DataItem` debe ser de tipo [ColumnBinding](binding-data-type-assl.md)|  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  