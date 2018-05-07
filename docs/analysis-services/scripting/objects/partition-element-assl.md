---
title: Crear particiones de elemento (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c0b1ecb715ec079144cfcfbd151722c1c9122b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="partition-element-assl"></a>Elemento Partition (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define una partición de un elemento [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) o una partición que enlaza un elemento [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md) dentro y fuera de línea.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Partitions>  
      <Partition> <!-- ancestor: MeasureGroup -->  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Source>...</Source>  
      <ProcessingPriority>...</ProcessingPriority>  
      <AggregationPrefix>...</AggregationPrefix>  
      <StorageMode>...</StorageMode>  
      <ProcessingMode>...</ProcessingMode>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <StorageLocation>...</StorageLocation>  
      <RemoteDatasourceID>...</RemoteDatasourceID>  
      <Slice>...</Slice>  
      <ProactiveCaching>...</ProactiveCaching>  
      <Type>...</Type>  
      <EstimatedSize>...</EstimatedSize>  
      <EstimatedRows>...</EstimatedRows>  
      <CurrentStorageMode>...</CurrentStorageMode>  
      <AggregationDesignID>...</AggregationDesignID>  
      <AggregationInstances>...</AggregationInstances>  
      <AggregationInstanceSource>...</AggregationInstanceSource>  
      <LastProcessed>...</LastProcessed>  
      <State>...</State>  
      <Annotations>.../Annotations>  
   </Partition>  
   <!-- or -->  
   <Partition xsi:type="PartitionBinding"> <!-- ancestor: MeasureGroupBinding -->  
   </Partition>  
</Partitions>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Vea la tabla siguiente.|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|Ninguno|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Particiones](../../../analysis-services/scripting/collections/partitions-element-assl.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md), [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md), [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md), [Description](../../../analysis-services/scripting/properties/description-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md), [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [Name](../../../analysis-services/scripting/properties/name-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md), [Slice](../../../analysis-services/scripting/properties/slice-element-assl.md), [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [State](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [Type](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Este elemento tiene las validaciones siguientes en el valor 2 (modo de servidor tabular) de DeploymentMode:  
  
-   Los siguientes elementos secundarios no se admiten y no se deberían utilizar:  
  
    -   [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md)  
  
    -   [Segmento](../../../analysis-services/scripting/properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)  
  
    -   [Tipo](../../../analysis-services/scripting/properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md)  
  
    -   [AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md)  
  
     Se puede producir un error si se utiliza alguno de los elementos anteriores.  
  
-   El elemento [Source](../../../analysis-services/scripting/properties/source-element-binding-assl.md) solo acepta enlaces de **consultas** .  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
