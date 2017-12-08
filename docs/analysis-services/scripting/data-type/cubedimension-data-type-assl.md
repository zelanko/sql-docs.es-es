---
title: Tipo de datos CubeDimension (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
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
apiname: CubeDimension Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeDimension
helpviewer_keywords: CubeDimension data type
ms.assetid: 128ac790-65a1-4e35-b909-8dba2a61b24c
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 63ce4755b2cf28ec2805b8e0eb32121b399816ab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[AllMemberAggregationUsage](../../../analysis-services/scripting/properties/allmemberaggregationusage-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md), [DimensionID](../../../analysis-services/scripting/properties/dimensionid-element-assl.md), [jerarquías](../../../analysis-services/scripting/collections/hierarchies-element-assl.md), [HierarchyUniqueNameStyle](../../../analysis-services/scripting/properties/hierarchyuniquenamestyle-element-assl.md), [identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [MemberUniqueNameStyle](../../../analysis-services/scripting/properties/memberuniquenamestyle-element-assl.md), [nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [Visible](../../../analysis-services/scripting/properties/visible-element-assl.md), [Traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|Elementos derivados|[Dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md) ([dimensiones](../../../analysis-services/scripting/collections/dimensions-element-assl.md) colección de [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 Hay un **CubeDimension** para cada relación de la dimensión en un **Cube**. **CubeDimension** abarca todo el **MeasureGroups** del cubo.  
  
 A **CubeDimension** debe incluir un [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md) si la dimensión tiene algo concreto que decir sobre la jerarquía, incluida la deshabilitación de la jerarquía (por lo tanto, lo que permite la selección de los cuales las jerarquías se aplican al uso de una dimensión concreta), o hacer que la jerarquía sea invisible.  
  
 De forma similar, un **CubeDimension** debe incluir un [CubeAttribute](../../../analysis-services/scripting/data-type/cubeattribute-data-type-assl.md) solo si la dimensión tiene algo concreto que decir sobre el atributo. (No hay ninguna manera de seleccionar qué atributos se aplicarán al uso de una dimensión concreta, aunque es posible hacer que los atributos no estén visibles).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
