---
title: Tipo de datos CubeAttribute (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11a45e49fa902554aaa2b7be1486fb976f03c580
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032146"
---
# <a name="cubeattribute-data-type-assl"></a>Tipo de datos CubeAttribute (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo que representa a un atributo asociado con un elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) .  
  
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
|Elementos secundarios|[AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md), [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md), [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md), [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|  
|Elementos derivados|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) (colección[Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) de [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El *AttributeHierarchyOptimizedState* elemento no se admite cuando se ejecuta el servicio en los valores de propiedad de configuración DeploymentMode 1 o 2 (modos SharePoint o Tabular, utilizados para ejecutar [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y modelo tabular bases de datos).  
  
 Un atributo no se puede agregar como un nivel de una jerarquía cuando la propiedad, *AtttributeHierarchyEnabled*, se establece en FALSE y la instancia está ejecutando debajo de DeploymentMode 1 o 2 (modo de servidor tabular o SharePoint).  
  
 Los atributos del elemento [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md) que no están incluidos explícitamente en la colección [Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) entran a formar parte de la colección y tienen asignados los valores predeterminados. Una vez agregados los atributos a la colección, el método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) puede devolverlos.  
  
 El elemento [AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md) controla el modo en que [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] diseña automáticamente las agregaciones para el atributo. El elemento **AggregationUsage** no restringe ninguna agregación que se crea manualmente para el cubo.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.CubeAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
