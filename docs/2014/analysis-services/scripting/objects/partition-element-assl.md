---
title: Elemento (ASSL) de partición | Microsoft Docs
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
- Partition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PARTITION
helpviewer_keywords:
- Partition element
ms.assetid: 40020840-1bb7-478f-9017-1a30342ac4c6
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c298ec80f1bb1f17d97e36f2ce93b6efbf924508
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209975"
---
# <a name="partition-element-assl"></a>Elemento Partition (ASSL)
  Define una partición de un [MeasureGroup](group-element-assl.md) elemento o una partición que enlaza un fuera de línea [MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md) elemento.  
  
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
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[MeasureGroup](group-element-assl.md)|None|  
|[MeasureGroupBinding](../data-type/binding-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Particiones](../collections/partitions-element-assl.md)|  
  
|Antecesor o elemento primario|Elementos secundarios|  
|------------------------|--------------------|  
|[MeasureGroup](../properties/id-element-assl.md), [AggregationInstances](../collections/aggregationinstances-element-assl.md), [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md), [AggregationPrefix](../properties/aggregationprefix-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [CurrentStorageMode](../properties/storagemode-element-assl.md), [descripción](../properties/description-element-assl.md), [ErrorConfiguration](errorconfiguration-element-assl.md), [EstimatedRows](../properties/estimatedrows-element-assl.md), [EstimatedSize](../properties/estimatedsize-element-assl.md), [ID](../properties/id-element-assl.md), [LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [Nombre](../properties/name-element-assl.md), [ProactiveCaching](proactivecaching-element-assl.md), [ProcessingMode](../properties/processingmode-element-assl.md), [ProcessingPriority](../properties/processingpriority-element-assl.md), [ RemoteDatasourceID](../properties/datasourceid-element-assl.md), [segmento](../properties/slice-element-assl.md), [origen](../properties/source-element-binding-assl.md), [estado](../properties/state-element-assl.md), [StorageLocation](../properties/storagelocation-element-assl.md), [ StorageMode](../properties/storagemode-element-assl.md), [tipo](../properties/type-element-partition-assl.md)|  
|[MeasureGroupBinding](../data-type/measuregroupbinding-data-type-out-of-line-assl.md)|None|  
  
## <a name="remarks"></a>Notas  
 Este elemento tiene las validaciones siguientes en el valor 2 (modo de servidor tabular) de DeploymentMode:  
  
-   Los siguientes elementos secundarios no se admiten y no se deberían utilizar:  
  
    -   [ProcessingPriority](../properties/processingpriority-element-assl.md)  
  
    -   [AggregationPrefix](../properties/aggregationprefix-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [ProcessingMode](../properties/processingmode-element-assl.md)  
  
    -   [ErrorConfiguration](errorconfiguration-element-assl.md)  
  
    -   [StorageLocation](../properties/storagelocation-element-assl.md)  
  
    -   [RemoteDatasourceID](../properties/datasourceid-element-assl.md)  
  
    -   [Segmento](../properties/slice-element-assl.md)  
  
    -   [ProactiveCaching](proactivecaching-element-assl.md)  
  
    -   [Tipo](../properties/type-element-partition-assl.md)  
  
    -   [CurrentStorageMode](../properties/storagemode-element-assl.md)  
  
    -   [AggregationDesignID](../properties/aggregationdesignid-element-assl.md)  
  
    -   [AggregationInstances](../collections/aggregationinstances-element-assl.md)  
  
    -   [AggregationInstanceSource](../properties/aggregationinstancesource-element-assl.md)  
  
     Se puede producir un error si se utiliza alguno de los elementos anteriores.  
  
-   El [origen](../properties/source-element-binding-assl.md) solo acepta el elemento **consulta** enlace.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
