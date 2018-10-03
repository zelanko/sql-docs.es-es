---
title: Referencia técnica para las anotaciones de Business Intelligence en CSDL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e0a166f1c81b9e010d7e9cfd7a0547c3a4b9c72
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094195"
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>Referencia técnica para las anotaciones de Business Intelligence en CSDL
  En esta sección se enumeran los elementos, los atributos y las propiedades de CSDL que se utilizan para representar los modelos tabulares de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Algunos elementos son nuevos; otros se han anotado o extendido para que admitan los modelos de Business Intelligence.  
  
 Para obtener información general de los modelos tabulares y cómo se representan las entidades, relaciones y fórmulas en CSDL, vea [anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="extended-csdl-elements-complex-types"></a>Elementos de CSDL extendidos: tipos complejos  
 Los elementos de CSDL siguientes se han agregado o extendido para admitir los modelos de datos de Business Intelligence, tanto tabulares como multidimensionales.  
  
-   [Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)  
  
-   [BaseProperty, elemento &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [Elemento DefaultDetails &#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)  
  
-   [Elemento DisplayKey &#40;CSDLBI&#41;](displaykey-element-csdlbi.md)  
  
-   [Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)  
  
-   [Elemento EntitySet &#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
-   [Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)  
  
-   [Elemento Hierarchy &#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)  
  
-   [Elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
-   [Elemento KpiGoal &#40;CSDLBI&#41;](kpigoal-element-csdlbi.md)  
  
-   [Elemento KpiStatus &#40;CSDLBI&#41;](kpistatus-element-csdlbi.md)  
  
-   [Elemento de nivel &#40;CSDLBI&#41;](level-element-csdlbi.md)  
  
-   [Elemento de medida &#40;CSDLBI&#41;](measure-element-csdlbi.md)  
  
-   [Elemento Member &#40;CSDLBI&#41;](member-element-csdlbi.md)  
  
-   [Elemento MemberRef &#40;CSDLBI&#41;](memberref-element-csdlbi.md)  
  
-   [Elemento NavigationProperty &#40;CSDLBI&#41;](navigationproperty-element-csdlbi.md)  
  
-   [Elemento de propiedad &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [PropertyRef, elemento &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>Tipo simple y subtipos  
 En la tabla siguiente se enumeran algunos tipos simples y algunos tipos complejos menores incluidos en las definiciones de los tipos complejos enumerados anteriormente. La documentación de cada tipo simple o subtipo que aparece en la columna izquierda se incluye en los elementos primarios incluidos en la columna derecha.  
  
|Tipo simple|Se encuentra en el tema|  
|-----------------|--------------------|  
|Alignment|[BaseProperty, elemento &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|CompareOptions|[Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|Contenido|[Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Elemento Member &#40;CSDLBI&#41;](member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Elemento de propiedad &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|DirectQueryMode|[Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Elemento de propiedad &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|MemberRefs|[Elemento MemberRef &#40;CSDLBI&#41;](memberref-element-csdlbi.md)|  
|PropertyRefs|[PropertyRef, elemento &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)|  
|SortDirection|[BaseProperty, elemento &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|State|[Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
|Stability|[Elemento de propiedad &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|SortDirection|[BaseProperty, elemento &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de CSDLBI](../csdlbi-concepts.md)  
  
  
