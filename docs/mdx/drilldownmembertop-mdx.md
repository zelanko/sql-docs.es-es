---
title: DrilldownMemberTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ebb3054ab25729ef5d75034dbee1d720f4dd928
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68031241"
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
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *Hierarchy*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Recursiva*  
 Palabra clave que indica comparación recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Palabra clave para que los miembros calculados puedan estar incluidos en la obtención de detalles.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión numérica, la función **DrilldownMemberTop** ordena, en orden descendente, los elementos secundarios de cada miembro del primer conjunto de acuerdo con el valor de la expresión numérica, según se ha evaluado sobre el conjunto de miembros secundarios. Si no se especifica una expresión numérica, la función clasifica, en orden descendente, los elementos secundarios de cada miembro del primer conjunto de acuerdo con los valores de las celdas representadas por el conjunto de miembros secundarios, según determine el contexto de consulta. Este comportamiento es similar a las funciones TopCount y Head (MDX) que devuelven un conjunto de miembros en orden natural, sin ninguna ordenación.  
  
 Después de la ordenación, la función **DrilldownMemberTop** devuelve un conjunto que contiene los miembros primarios y el número de miembros secundarios, especificados en *Count,* con el valor más alto y se incluyen en ambos conjuntos.  
  
 Si se especifica **Recursive** , la función ordena el primer conjunto como se ha descrito anteriormente y, a continuación, compara de forma recursiva los miembros del primer conjunto, organizados en una jerarquía, en el segundo conjunto. La función recupera el número superior de elementos secundarios de cada miembro del primer conjunto que también está presente en el segundo conjunto.  
  
 El primer conjunto puede contener tuplas en vez de miembros. La obtención de detalles de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en lugar de miembros.  
  
 La función **DrilldownMemberTop** es similar a la función [DrilldownMember](../mdx/drilldownmember-mdx.md) , pero en lugar de incluir todos los elementos secundarios de cada miembro del primer conjunto que también está presente en el segundo conjunto, la función **DrilldownMemberTop** devuelve el número más alto de miembros secundarios de cada miembro.  
  
 La consulta de la propiedad XMLA MdpropMdxDrillFunctions permite comprobar el nivel de compatibilidad que el servidor proporciona para las funciones de perforación. para más información, consulte [las propiedades XMLA compatibles &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
