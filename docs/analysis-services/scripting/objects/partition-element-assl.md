---
title: Crear particiones de elemento (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Partition Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 81f97678d2c741768a3f9b4201b288f738f603fe
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="partition-element-assl"></a>Elemento Partition (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Define una partición de un [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md) elemento o una partición que enlaza un fuera de línea [MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md) elemento.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Vea la siguiente tabla.|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|None|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Particiones](../../../analysis-services/scripting/collections/partitions-element-assl.md)|  
|Elementos secundarios|Vea la siguiente tabla.|  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)|[AggregationDesignID](../../../analysis-services/scripting/properties/aggregationdesignid-element-assl.md), [AggregationInstances](../../../analysis-services/scripting/collections/aggregationinstances-element-assl.md), [AggregationInstanceSource](../../../analysis-services/scripting/properties/aggregationinstancesource-element-assl.md), [AggregationPrefix](../../../analysis-services/scripting/properties/aggregationprefix-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [CurrentStorageMode](../../../analysis-services/scripting/properties/currentstoragemode-element-assl.md), [descripción](../../../analysis-services/scripting/properties/description-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [ EstimatedRows](../../../analysis-services/scripting/properties/estimatedrows-element-assl.md), [EstimatedSize](../../../analysis-services/scripting/properties/estimatedsize-element-assl.md), [identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ Nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md), [ProcessingMode](../../../analysis-services/scripting/properties/processingmode-element-assl.md), [ProcessingPriority](../../../analysis-services/scripting/properties/processingpriority-element-assl.md), [RemoteDatasourceID](../../../analysis-services/scripting/properties/remotedatasourceid-element-assl.md), [Segmento](../../../analysis-services/scripting/properties/slice-element-assl.md), [origen](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [estado](../../../analysis-services/scripting/properties/state-element-assl.md), [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md), [StorageMode](../../../analysis-services/scripting/properties/storagemode-element-assl.md), [Tipo](../../../analysis-services/scripting/properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../../../analysis-services/scripting/data-type/measuregroupbinding-data-type-out-of-line-assl.md)|None|  
  
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
  
-   El [origen](../../../analysis-services/scripting/properties/source-element-binding-assl.md) el elemento solo acepta **consulta** enlace.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
