---
title: DrilldownMemberTop (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f2e055d0d05d6c111b52d2f23f3248e96de11966
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740854"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  Aumenta el nivel de detalle de miembros de un conjunto especificado que están presentes en otro conjunto especificado, lo que limita el conjunto de resultados a un número específico de miembros. O bien, esta función obtiene detalles de un conjunto de tuplas usando la primera jerarquía de la tupla o la jerarquía especificada opcionalmente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recuento*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *Hierarchy*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Recursiva*  
 Palabra clave que indica comparación recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Palabra clave para que los miembros calculados puedan estar incluidos en la obtención de detalles.  
  
## <a name="remarks"></a>Notas  
 Si se especifica una expresión numérica, la **DrilldownMemberTop** función clasifica, en orden descendente, los elementos secundarios de cada miembro del primer conjunto según el valor de la expresión numérica, según se ha evaluado sobre el conjunto de miembros secundarios. Si no se especifica una expresión numérica, la función clasifica, en orden descendente, los elementos secundarios de cada miembro del primer conjunto de acuerdo con los valores de las celdas representadas por el conjunto de miembros secundarios, según determine el contexto de consulta. Este comportamiento es similar a las funciones TopCount y Head (MDX) que devuelven un conjunto de miembros en orden natural, sin ninguna ordenación.  
  
 Tras realizar la clasificación, el **DrilldownMemberTop** función devuelve un conjunto que contiene los miembros primarios y el número de miembros secundarios especificados en *recuento,* con el valor más alto y que están incluidos en ambos conjuntos.  
  
 Si **RECURSIVA** se especifica, la función ordena el primer conjunto como se describió anteriormente, a continuación, compara de forma recursiva los miembros del primer conjunto, organizados en una jerarquía, con el segundo conjunto *.* La función recupera el número más alto de los elementos secundarios de cada miembro del primer conjunto que también están presentes en el segundo conjunto.  
  
 El primer conjunto puede contener tuplas en vez de miembros. Obtención de detalles de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en vez de miembros.  
  
 El **DrilldownMemberTop** función es similar a la [DrilldownMember](../mdx/drilldownmember-mdx.md) funcionando, pero en lugar de incluir todos los elementos secundarios de cada miembro del primer conjunto que también están presentes en el segundo conjunto, la **DrilldownMemberTop** función devuelve el número de miembros secundarios de cada miembro del nivel superior.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones obtener detalles. vea [admite propiedades XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obtener más información.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se explora en profundidad la categoría de ropa para devolver las tres subcategorías de ropa con la mayor cantidad de pedidos enviados.  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
