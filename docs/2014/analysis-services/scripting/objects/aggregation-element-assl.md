---
title: Elemento Aggregation (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Aggregation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Aggregation
helpviewer_keywords:
- Aggregation element
ms.assetid: f37af388-b2b3-4234-a1d6-936ee9b7f2ae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0780a8c81cf80871eed925471fd0ea7e6103e9b6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167805"
---
# <a name="aggregation-element-assl"></a>Elemento Aggregation (ASSL)
  Define una agregación única para un [partición](partition-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Aggregations>  
      <Aggregation>  
      <ID>...</ID>  
      <Name>...</Name>  
      <Dimensions>...</Dimensions>  
            <Annotations>...</Annotations>  
      <Description>...</Description>  
   </Aggregation>  
</Aggregations>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Agregaciones](../collections/aggregations-element-assl.md)|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [descripción](../properties/description-element-assl.md), [dimensiones](../collections/dimensions-element-assl.md), [ID](../properties/id-element-assl.md), [nombre](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Aggregation>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de la partición &#40;ASSL&#41;](partition-element-assl.md)   
 [Elemento AggregationDesign &#40;ASSL&#41;](aggregationdesign-element-assl.md)   
 [Elemento MeasureGroup &#40;ASSL&#41;](group-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
