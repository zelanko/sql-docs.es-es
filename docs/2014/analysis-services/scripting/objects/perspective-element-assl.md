---
title: Elemento Perspective (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Perspective Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Perspective
helpviewer_keywords:
- Perspective element
ms.assetid: 0442334c-8b00-4451-ad81-02e58c735e8f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ed510b7c4b9a9c023c6bad875ed2e6293ac2ac4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168235"
---
# <a name="perspective-element-assl"></a>Elemento Perspective (ASSL)
  Define los detalles de una perspectiva de un [cubo](cube-element-assl.md) elemento.  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Perspectivas](../collections/perspectives-element-assl.md)|  
|Elementos secundarios|[Acciones](../collections/actions-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [cálculos](../collections/calculations-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [DefaultMeasure](measure-element-assl.md), [ Descripción](../properties/description-element-assl.md), [dimensiones](../collections/dimensions-element-assl.md), [ID](../properties/id-element-assl.md), [KPI](../collections/kpis-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [ MeasureGroups](../collections/groups-element-assl.md), [nombre](../properties/name-element-assl.md), [traducciones](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Una perspectiva proporciona un subconjunto de un cubo, seleccionando las dimensiones, jerarquías, atributos y otros detalles que se deben incluir y definiendo el segmento de datos que se debe incluir. Un solo cubo es el propietario de una perspectiva. No es posible invalidar o agregar objetos dentro de una perspectiva; todas las dimensiones, jerarquías y otros detalles deben existir en el cubo subyacente. No es posible incluir objetos y marcarlos como no visibles.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Perspective>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
