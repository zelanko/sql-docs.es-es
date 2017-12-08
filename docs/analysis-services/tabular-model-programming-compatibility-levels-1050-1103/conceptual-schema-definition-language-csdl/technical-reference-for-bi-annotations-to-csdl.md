---
title: "Referencia técnica de anotaciones de BI para CSDL | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 525b00678272347473f0cf845689be6d691c8ace
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>Referencia técnica para las anotaciones de Business Intelligence en CSDL
  En esta sección se enumeran los elementos, los atributos y las propiedades de CSDL que se utilizan para representar los modelos tabulares de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Algunos elementos son nuevos; otros se han anotado o extendido para que admitan los modelos de Business Intelligence.  
  
 Para obtener información general de los modelos tabulares y cómo se representan las entidades, relaciones y fórmulas en CSDL, vea [anotaciones de CSDL para Business Intelligence &#40; CSDLBI &#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
## <a name="extended-csdl-elements-complex-types"></a>Elementos de CSDL extendidos: tipos complejos  
 Los elementos de CSDL siguientes se han agregado o extendido para admitir los modelos de datos de Business Intelligence, tanto tabulares como multidimensionales.  
  
-   [AssociationSet, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)  
  
-   [BaseProperty, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)  
  
-   [DefaultDetails, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md)  
  
-   [DisplayKey, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md)  
  
-   [EntityContainer, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)  
  
-   [EntitySet, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
-   [EntityType, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)  
  
-   [Hierarchy, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md)  
  
-   [KPI, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
-   [Kpigoal, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpigoal-element-csdlbi.md)  
  
-   [Kpistatus, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpistatus-element-csdlbi.md)  
  
-   [Level, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/level-element-csdlbi.md)  
  
-   [Measure, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/measure-element-csdlbi.md)  
  
-   [Member, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/member-element-csdlbi.md)  
  
-   [MemberRef, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md)  
  
-   [NavigationProperty, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/navigationproperty-element-csdlbi.md)  
  
-   [Elemento Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)  
  
-   [PropertyRef, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>Tipo simple y subtipos  
 En la tabla siguiente se enumeran algunos tipos simples y algunos tipos complejos menores incluidos en las definiciones de los tipos complejos enumerados anteriormente. La documentación de cada tipo simple o subtipo que aparece en la columna izquierda se incluye en los elementos primarios incluidos en la columna derecha.  
  
|Tipo simple|Se encontró en el tema|  
|-----------------|--------------------|  
|Alignment|[BaseProperty, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
|CompareOptions|[EntityContainer, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)|  
|Contenido|[EntityType, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Member, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/member-element-csdlbi.md)|  
|DefaultAggregationFunction|[Elemento Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|DirectQueryMode|[EntityContainer, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[Elemento Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|MemberRefs|[MemberRef, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md)|  
|PropertyRefs|[PropertyRef, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)|  
|SortDirection|[BaseProperty, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
|State|[AssociationSet, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
|Stability|[Elemento Property &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/property-element-csdlbi.md)|  
|SortDirection|[BaseProperty, elemento &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/baseproperty-element-csdlbi.md)|  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de CSDLBI](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  
