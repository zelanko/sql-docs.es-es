---
title: Elemento Perspective (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Perspective Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Perspective
helpviewer_keywords:
- Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d11ad3d42057ac3d90eb821dd12a6988dd157e4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="perspective-element-assl"></a>Elemento Perspective (ASSL)
  Define los detalles de una perspectiva de un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Perspectives>  
   <<Perspective>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Description>...</Description>  
      <Translations>...</Translations>  
      <DefaultMeasure>...</DefaultMeasure>  
      <Dimensions>...</Dimensions>  
            <MeasureGroups>...</MeasureGroups>  
      <Calculations>...</Calculations>  
      <Kpis>...</Kpis>  
            <Actions>...</Actions>  
      <Annotations>...</Annotations>  
   </Perspective>  
</Perspectives>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Perspectivas](../../../analysis-services/scripting/collections/perspectives-element-assl.md)|  
|Elementos secundarios|[Acciones](../../../analysis-services/scripting/collections/actions-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [cálculos](../../../analysis-services/scripting/collections/calculations-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [DefaultMeasure](../../../analysis-services/scripting/properties/defaultmeasure-element-assl.md), [ Descripción](../../../analysis-services/scripting/properties/description-element-assl.md), [dimensiones](../../../analysis-services/scripting/collections/dimensions-element-assl.md), [identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [KPI](../../../analysis-services/scripting/collections/kpis-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [ MeasureGroups](../../../analysis-services/scripting/collections/measuregroups-element-assl.md), [nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Una perspectiva proporciona un subconjunto de un cubo, seleccionando las dimensiones, jerarquías, atributos y otros detalles que se deben incluir y definiendo el segmento de datos que se debe incluir. Un solo cubo es el propietario de una perspectiva. No es posible invalidar o agregar objetos dentro de una perspectiva; todas las dimensiones, jerarquías y otros detalles deben existir en el cubo subyacente. No es posible incluir objetos y marcarlos como no visibles.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

