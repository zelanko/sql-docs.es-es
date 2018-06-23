---
title: Tipo de datos CubeDimension (ASSL) | Documentos de Microsoft
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
- CubeDimension Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeDimension
helpviewer_keywords:
- CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4a043895929e09a59d3ae14c5995804c4fa5c7eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103947"
---
# <a name="cubedimension-data-type-assl"></a>Tipo de datos CubeDimension (ASSL)
  Define un tipo de datos primitivo que representa la relación existente entre una dimensión y un cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeDimension>  
      <ID>...</ID>  
   <Name>...</Name>  
   <Translations>...</Translations>  
   <DimensionID>...</DimensionID>  
   <Visible>...</Visible>  
   <AllMemberAggregationUsage>...</AllMemberAggregationUsage>  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   <MemberUniqueNameStyle>...</MemberUniqueNameStyle>  
      <Attributes>...</Attributes>  
   <Hierarchies>...</Hierarchies>  
      <Annotations>...</Annotation>  
</CubeDimension>  
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
|Elementos secundarios|[AllMemberAggregationUsage](../properties/aggregationusage-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [atributos](../collections/attributes-element-assl.md), [DimensionID](../properties/id-element-assl.md), [jerarquías](../collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../properties/hierarchyuniquenamestyle-element-assl.md), [identificador](../properties/id-element-assl.md), [MemberUniqueNameStyle](../properties/memberuniquenamestyle-element-assl.md), [nombre](../properties/name-element-assl.md), [Visible](../properties/visible-element-assl.md), [Traducciones](../collections/translations-element-assl.md)|  
|Elementos derivados|[Dimensión](../objects/dimension-element-assl.md) ([dimensiones](../collections/dimensions-element-assl.md) colección de [cubo](../objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Notas  
 Hay un `CubeDimension` para cada relación de la dimensión en un `Cube`. `CubeDimension` abarca todo el `MeasureGroups` del cubo.  
  
 A `CubeDimension` debe incluir un [CubeHierarchy](hierarchy-data-type-assl.md) si la dimensión tiene algo concreto que decir sobre la jerarquía, incluida la deshabilitación de la jerarquía (por lo tanto, que permita la selección de los cuales jerarquías se aplican a un determinado uso de dimensiones), o hacer que la jerarquía sea invisible.  
  
 De forma similar, un `CubeDimension` debe incluir un [CubeAttribute](cubeattribute-data-type-assl.md) solo si la dimensión tiene algo concreto que decir sobre el atributo. (No hay ninguna manera de seleccionar qué atributos se aplicarán al uso de una dimensión concreta, aunque es posible hacer que los atributos no estén visibles).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  