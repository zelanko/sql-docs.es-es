---
title: DrilldownMemberBottom (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DRILLDOWNMEMBERBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownMemberBottom function
ms.assetid: 603927ba-68f6-4e7a-b17f-44cad33bdfb0
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b740a78a8d8cd425587e568db4a7cae521ad78e9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Aumenta el nivel de detalle de miembros de un conjunto especificado que están presentes en otro conjunto especificado, lo que limita el conjunto de resultados a un número específico de miembros. Alternativamente, esta función detalla un conjunto de tuplas usando la primera jerarquía de la tupla o la jerarquía especificada opcionalmente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Count*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *Jerarquía de*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Recursiva*  
 Palabra clave que indica comparación recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Palabra clave para que los miembros calculados puedan estar incluidos en la obtención de detalles.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, la **DrilldownMemberBottom** función clasifica, en orden ascendente, los elementos secundarios de cada miembro del primer conjunto, según el valor de la expresión numérica, según se ha evaluado sobre el conjunto de miembros secundarios. Si no se especifica una expresión numérica, la función clasifica, en orden ascendente, los elementos secundarios de cada miembro del primer conjunto de acuerdo con los valores de las celdas representadas por el conjunto de miembros secundarios, según determina el contexto de la consulta. Este comportamiento es similar a las funciones Tail (MDX) y BottomCount que devuelven un conjunto de miembros en orden natural, sin ninguna ordenación.  
  
 Tras realizar la clasificación, el **DrilldownMemberBottom** función devuelve un conjunto que contiene los miembros primarios y el número de miembros secundarios especificados en *recuento,* con el valor más bajo y que están contenidos en ambos conjuntos.  
  
 Si **RECURSIVA** se especifica, la función ordena el primer conjunto como se describió anteriormente, a continuación, compara de forma recursiva los miembros del primer conjunto, organizados en una jerarquía, con el segundo conjunto. La función recupera el número inferior de miembros secundarios de cada miembro del primer conjunto que también están presentes en el segundo conjunto.  
  
 El primer conjunto puede contener tuplas en vez de miembros. Obtención de detalles de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en vez de miembros.  
  
 El **DrilldownMemberBottom** función es similar a la [DrilldownMember](../mdx/drilldownmember-mdx.md) funcionando, pero en lugar de incluir todos los elementos secundarios de cada miembro del primer conjunto que también están presentes en el segundo conjunto, la **DrilldownMemberBottom** función devuelve el número más bajo de miembros secundarios de cada miembro.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones obtener detalles. vea [admite propiedades XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
