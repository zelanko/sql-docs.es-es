---
title: Elemento MeasureGroup (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
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
- MeasureGroup Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5232a3299f269d6f798523d934ca80cff21097df
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="measuregroup-element-assl"></a>Elemento MeasureGroup (ASSL)
  Define un conjunto de medidas en el mismo nivel de granularidad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MeasureGroups>  
   <MeasureGroup> <!-- ancestor: Cube -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</<Create  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Type>...</Type>  
      <State>...</State>  
      <MeasureQualification>...</MeasureQualification>  
      <Measures>...</Measures>  
      <DataAggregation>...</DataAggregation>  
      <Source>...</Source>  
            <StorageMode>...</StorageMode>  
      <StorageLocation>...</StorageLocation>  
      <IgnoreUnrelatedDimensions>...</IgnoreUnrelatedDimensions>  
            <ProactiveCaching>...</ProactiveCaching>  
      <EstimatedRows>...</EstimatedRows>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <EstimatedSize>...</EstimatedSize>  
      <ProcessingMode>...</ProcessingMode>  
      <Dimensions>...</Dimensions>  
      <Partitions>...</Partitions>  
      <AggregationPrefix>...</AggregationPrefix>  
      <ProcessingPriority>...</ProcessingPriority>  
            <AggregationDesigns>...</AggregationDesigns>  
      <Annotations>...</Annotations>  
   </MeasureGroup>  
   <!-- or  -->  
   <MeasureGroup xsi:type="MeasureGroupBinding">...</MeasureGroup> <!-- ancestor: CubeBinding -->  
   <!-- or  -->  
   <MeasureGroup xsi:type="PerspectiveMeasureGroup">...</MeasureGroup> <!-- ancestor: Perspective -->  
</MeasureGroups>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Vea la siguiente tabla.|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md)|Ninguno|  
|[CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-assl.md)|  
|[Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveMeasureGroup](../../../analysis-services/scripting/data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MeasureGroup](../../../analysis-services/scripting/collections/measuregroups-element-assl.md)|  
|Elementos secundarios|Vea la siguiente tabla.|  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md)|[AggregationDesigns](../../../analysis-services/scripting/collections/aggregationdesigns-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [DataAggregation](../../../analysis-services/scripting/properties/dataaggregation-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [Dimensions](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [IgnoreUnrelatedDimensions](../../../analysis-services/scripting/properties/ignoreunrelateddimensions-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MeasureQualification](../../../analysis-services/scripting/properties/measurequalificaton-element-assl.md), [Measures](../../../analysis-services/scripting/collections/measures-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Partitions](../../../analysis-services/scripting/collections/partitions-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-measure-assl.md), [State](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [Translations](../../../analysis-services/scripting/collections/translations-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../../../analysis-services/scripting/data-type/cubebinding-data-type-out-of-line-assl.md)|Ninguno|  
|[Perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md)|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Todas las medidas de un grupo de medidas se deben originar en una tabla única. Un grupo de medidas puede definir enlaces predeterminados que se pueden invalidar para cada partición.  
  
 El elemento **MeasureGroup** define los detalles comunes para medir grupos en cubos normales y cubos virtuales. Los subtipos independientes definen los detalles concretos de cada tipo.  
  
 La propiedad **State** de **MeasureGroup** tiene los siguientes valores:  
  
-   *FullyProcessed* si se procesan todas las particiones.  
  
-   *PartiallyProcessed* si por lo menos se procesa una partición.  
  
-   *Unprocessed* si no se procesa ninguna partición.  
  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.MeasureGroup> y <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

