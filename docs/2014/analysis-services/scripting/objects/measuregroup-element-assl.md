---
title: Elemento MeasureGroup (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MeasureGroup Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MeasureGroup
helpviewer_keywords:
- MeasureGroup element
ms.assetid: 7aa099db-5dc7-4cac-b437-f73fc0921b24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84186a736f7d3e17587a3a5457b1c7850c02f12b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089715"
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
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[Cubo](cube-element-assl.md)|None|  
|[CubeBinding](../data-type/binding-data-type-assl.md)|  
|[Perspectiva](../data-type/perspectivemeasuregroup-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MeasureGroups](../collections/groups-element-assl.md)|  
|Elementos secundarios||  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[Cubo](../collections/aggregationdesigns-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [DataAggregation](aggregation-element-assl.md), [ Descripción](../properties/description-element-assl.md), [dimensiones](../collections/dimensions-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md), [EstimatedRows](../properties/estimatedrows-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [IgnoreUnrelatedDimensions](../properties/ignoreunrelateddimensions-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [ MeasureQualification](../properties/measurequalificaton-element-assl.md), [medidas](../collections/measures-element-assl.md), [nombre](../properties/name-element-assl.md), [particiones](../collections/partitions-element-assl.md), [ProactiveCaching](proactivecaching-element-assl.md), [ ProcessingMode](../properties/processingmode-element-assl.md), [ProcessingPriority](../properties/processingpriority-element-assl.md), [origen](../properties/source-element-measure-assl.md), [estado](../properties/state-element-assl.md), [StorageLocation](../properties/storagelocation-element-assl.md), [ StorageMode](../properties/storagemode-element-assl.md), [traducciones](../collections/translations-element-assl.md), [tipo](../properties/type-element-measuregroup-assl.md)|  
|[CubeBinding](../data-type/cubebinding-data-type-out-of-line-assl.md)|None|  
|[Perspectiva](perspective-element-assl.md)|None|  
  
## <a name="remarks"></a>Comentarios  
 Todas las medidas de un grupo de medidas se deben originar en una tabla única. Un grupo de medidas puede definir enlaces predeterminados que se pueden invalidar para cada partición.  
  
 El elemento `MeasureGroup` define los detalles comunes para medir grupos en cubos normales y cubos virtuales. Los subtipos independientes definen los detalles concretos de cada tipo.  
  
 La propiedad `State` de `MeasureGroup` tiene los siguientes valores:  
  
-   *FullyProcessed* si se procesan todas las particiones.  
  
-   *PartiallyProcessed* si por lo menos se procesa una partición.  
  
-   *Unprocessed* si no se procesa ninguna partición.  
  
 Los elementos correspondientes en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.MeasureGroup> y <xref:Microsoft.AnalysisServices.PerspectiveMeasureGroup>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
