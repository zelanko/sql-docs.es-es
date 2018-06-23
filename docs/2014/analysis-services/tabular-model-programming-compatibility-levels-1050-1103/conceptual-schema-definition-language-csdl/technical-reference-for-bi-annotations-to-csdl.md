---
title: Referencia técnica de anotaciones de BI para CSDL | Documentos de Microsoft
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
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 27ed1339d64dd3c4035288a96b31ae163a304733
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107497"
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>Referencia técnica para las anotaciones de Business Intelligence en CSDL
  En esta sección se enumeran los elementos, los atributos y las propiedades de CSDL que se utilizan para representar los modelos tabulares de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Algunos elementos son nuevos; otros se han anotado o extendido para que admitan los modelos de Business Intelligence.  
  
 Para obtener información general de los modelos tabulares y cómo se representan las entidades, relaciones y fórmulas en CSDL, vea [anotaciones de CSDL para Business Intelligence &#40;CSDLBI&#41;](../csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="extended-csdl-elements-complex-types"></a>Elementos de CSDL extendidos: tipos complejos  
 Los elementos de CSDL siguientes se han agregado o extendido para admitir los modelos de datos de Business Intelligence, tanto tabulares como multidimensionales.  
  
-   [Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)  
  
-   [Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [Elemento DefaultDetails &#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)  
  
-   [Elemento DisplayKey &#40;CSDLBI&#41;](displaykey-element-csdlbi.md)  
  
-   [Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)  
  
-   [Elemento EntitySet &#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
-   [Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)  
  
-   [Elemento de la jerarquía &#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)  
  
-   [Elemento KPI &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
-   [Elemento KpiGoal &#40;CSDLBI&#41;](kpigoal-element-csdlbi.md)  
  
-   [Elemento KpiStatus &#40;CSDLBI&#41;](kpistatus-element-csdlbi.md)  
  
-   [Elemento nivel &#40;CSDLBI&#41;](level-element-csdlbi.md)  
  
-   [Elemento de medida &#40;CSDLBI&#41;](measure-element-csdlbi.md)  
  
-   [Elemento Member &#40;CSDLBI&#41;](member-element-csdlbi.md)  
  
-   [Elemento MemberRef &#40;CSDLBI&#41;](memberref-element-csdlbi.md)  
  
-   [Elemento NavigationProperty &#40;CSDLBI&#41;](navigationproperty-element-csdlbi.md)  
  
-   [Elemento Property &#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [Elemento PropertyRef &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>Tipo simple y subtipos  
 En la tabla siguiente se enumeran algunos tipos simples y algunos tipos complejos menores incluidos en las definiciones de los tipos complejos enumerados anteriormente. La documentación de cada tipo simple o subtipo que aparece en la columna izquierda se incluye en los elementos primarios incluidos en la columna derecha.  
  
|Tipo simple|Se encontró en el tema|  
|-----------------|--------------------|  
|Alignment|[Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|CompareOptions|[Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|Contenido|[Elemento EntityType &#40;CSDLBI&#41;](entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Elemento Member &#40;CSDLBI&#41;](member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Elemento Property &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|DirectQueryMode|[Elemento EntityContainer &#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Elemento Property &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|MemberRefs|[Elemento MemberRef &#40;CSDLBI&#41;](memberref-element-csdlbi.md)|  
|PropertyRefs|[Elemento PropertyRef &#40;CSDLBI&#41;](propertyref-element-csdlbi.md)|  
|SortDirection|[Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|State|[Elemento AssociationSet &#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
|Stability|[Elemento Property &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|SortDirection|[Elemento BaseProperty &#40;CSDLBI&#41;](property-element-csdlbi.md)|  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de CSDLBI](../csdlbi-concepts.md)  
  
  