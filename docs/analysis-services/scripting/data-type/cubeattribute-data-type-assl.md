---
title: Tipo de datos CubeAttribute (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
apiname: CubeAttribute Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeAttribute
helpviewer_keywords: CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: "45"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 004ae803e654a8267b89bf5b5ab813052f7b3eda
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="cubeattribute-data-type-assl"></a>Tipo de datos CubeAttribute (ASSL)
  Define un tipo de datos primitivo que representa un atributo asociado con un [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) elemento.  
  
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
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md), [anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md), [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md), [ AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md), [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|  
|Elementos derivados|[Atributo](../../../analysis-services/scripting/objects/attribute-element-assl.md) ([atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md) colección de [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El *AttributeHierarchyOptimizedState* elemento no se admite cuando se ejecuta el servicio en los valores de propiedad de configuración DeploymentMode 1 o 2 (modos SharePoint o Tabular, utilizados para ejecutar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y modelo tabular bases de datos).  
  
 Un atributo no se puede agregar como un nivel de una jerarquía cuando la propiedad, *AtttributeHierarchyEnabled*, se establece en FALSE y la instancia está ejecutando debajo de DeploymentMode 1 o 2 (modo de servidor tabular o SharePoint).  
  
 Atributos de la [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md) elemento que no están incluidos explícitamente en el [atributos](../../../analysis-services/scripting/collections/attributes-element-assl.md) parte de la colección se convierten en de la colección con los valores predeterminados asignados. Una vez agregados los atributos a la colección, los atributos pueden ser devueltos por la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
 El [AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md) elemento controla cómo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] diseña automáticamente las agregaciones para el atributo. El elemento **AggregationUsage** no restringe ninguna agregación que se crea manualmente para el cubo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubeAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
