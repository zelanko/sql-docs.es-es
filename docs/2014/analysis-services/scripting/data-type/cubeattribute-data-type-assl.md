---
title: Tipo de datos CubeAttribute (ASSL) | Documentos de Microsoft
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
- CubeAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dce594145db99d7edfa991c2e975f62e55d3ef34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111032"
---
# <a name="cubeattribute-data-type-assl"></a>Tipo de datos CubeAttribute (ASSL)
  Define un tipo de datos primitivo que representa un atributo asociado con un [cubo](../objects/cube-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeAttribute>  
   <AttributeID>...</AttributeID>  
   <AggregationUsage>...</AggregationUsage>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <Annotations>...</Annotations>  
</CubeAttribute>  
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
|Elementos secundarios|[AggregationUsage](../properties/aggregationusage-element-assl.md), [anotaciones](../collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../properties/enabled-element-assl.md), [AttributeHierarchyOptimizedState](../properties/state-element-assl.md), [ AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeID](../properties/id-element-assl.md)|  
|Elementos derivados|[Atributo](../objects/attribute-element-assl.md) ([atributos](../collections/attributes-element-assl.md) colección de [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Notas  
 El elemento *AttributeHierarchyOptimizedState* no se admite al ejecutar el servicio con los valores de la propiedad de configuración DeploymentMode 1 o 2 (los modos SharePoint o tabular, que se usan para ejecutar bases de datos de modelo tabulares y PowerPivot).  
  
 Un atributo no se puede agregar como un nivel de una jerarquía cuando la propiedad, *AtttributeHierarchyEnabled*, se establece en FALSE y la instancia está ejecutando debajo de DeploymentMode 1 o 2 (modo de servidor tabular o SharePoint).  
  
 Atributos de la [CubeDimension](dimension-data-type-assl.md) elemento que no están incluidos explícitamente en el [atributos](../collections/attributes-element-assl.md) parte de la colección se convierten en de la colección con los valores predeterminados asignados. Una vez agregados los atributos a la colección, los atributos pueden ser devueltos por la [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 El [AggregationUsage](../properties/aggregationusage-element-assl.md) elemento controla cómo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] diseña automáticamente las agregaciones para el atributo. El elemento `AggregationUsage` no restringe ninguna agregación que se crea manualmente para el cubo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubeAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  