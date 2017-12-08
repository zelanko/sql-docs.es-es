---
title: Medir el elemento (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
apiname: Measure Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Measure
helpviewer_keywords: Measure element
ms.assetid: 4c2c2ed1-7f78-4564-982a-132f13bea36f
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9942b67b7877e337f34667b90a49bd7c33595592
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="measure-element-assl"></a>Elemento Measure (ASSL)
  Define una medida.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Measures>  
   <Measure> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <AggregateFunction>...</AggregateFunction>  
            <DataType>...</DataType>  
            <Source>...</Source>  
      <Visible>...</Visible>  
      <MeasureExpression>...</MeasureExpression>  
      <DisplayFolder>...</DisplayFolder>  
      <FormatString>...</FormatString>  
      <BackColor>...</BackColor>  
      <ForeColor>...</ForeColor>  
            <FontName>...</FontName>  
            <FontSize>...</FontSize>  
            <FontFlags>...</FontFlags>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Measure>  
   <!-- or  -->  
   <Measure xsi:type="AggregationInstanceMeasure">...</Measure> <!-- parent: AggregationInstance -->  
      <!-- or  -->  
   <Measure xsi:type="MeasureBinding">...</Measure> <!-- ancestor: MeasureGroupBinding (out-of-line) -->  
   <!-- or  -->  
   <Measure xsi:type="PerspectiveMeasure">...</Measure> <!-- ancestor: PerspectiveMeasureGroup -->  
</Measures>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Vea la siguiente tabla.|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[AggregationInstance](../../../analysis-services/scripting/objects/aggregationinstance-element-assl.md)|[AggregationInstanceMeasure](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Ninguno|  
|[MeasureGroupBinding (fuera de línea)](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[MeasureBinding](../../../analysis-services/scripting/data-type/measurebinding-data-type-assl.md)|  
|[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|[PerspectiveMeasure](../../../analysis-services/scripting/data-type/perspectivemeasure-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Medidas](../../../analysis-services/scripting/collections/measures-element-assl.md)|  
|Elementos secundarios|Vea la siguiente tabla.|  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[AggregateFunction](../../../analysis-services/scripting/properties/aggregatefunction-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [BackColor](../../../analysis-services/scripting/properties/backcolor-element-assl.md), [DataType](../../../analysis-services/scripting/properties/datatype-element-assl.md), [descripción](../../../analysis-services/scripting/properties/description-element-assl.md), [ DisplayFolder](../../../analysis-services/scripting/properties/displayfolder-element-assl.md), [FontFlags](../../../analysis-services/scripting/properties/fontflags-element-assl.md), [FontName](../../../analysis-services/scripting/properties/fontname-element-assl.md), [FontSize](../../../analysis-services/scripting/properties/fontsize-element-assl.md), [ForeColor](../../../analysis-services/scripting/properties/forecolor-element-assl.md), [ FormatString](../../../analysis-services/scripting/properties/formatstring-element-assl.md), [identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [MeasureExpression](../../../analysis-services/scripting/properties/measureexpression-element-assl.md), [nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [origen](../../../analysis-services/scripting/properties/source-element-measure-assl.md), [ Traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md), [Visible](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|Todos las demás|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Se pueden proporcionar detalles de enlace para una medida. Estos detalles actúan después como los valores predeterminados para la partición.  
  
 En los cubos más grandes, puede haber cientos de medidas y jerarquías. La propiedad **DisplayFolder** define la apariencia del usuario en el cliente. El valor de la propiedad **DisplayFolder** puede contener cualquiera de las opciones siguientes:  
  
-   Puede estar vacío, lo que indica que la medida no pertenece a una carpeta.  
  
-   Puede contener un único nombre de carpeta, lo que indica que la medida debería representarse como perteneciente a una carpeta con el mismo nombre.  
  
-   Contienen varios nombres de carpeta separados por una barra diagonal inversa (\\), lo que indica una jerarquía de carpetas incrustada.  
  
 La propiedad **DisplayFolder** se aplica también a medidas y jerarquías calculadas.  
  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.Measure> y <xref:Microsoft.AnalysisServices.PerspectiveMeasure>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
