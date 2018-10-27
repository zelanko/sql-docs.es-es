---
title: DrilldownLevelBottom (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14b0b2dfd3e4578558e49cc305c37821e208c65d
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144940"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


  Aumenta el detalle de los miembros inferiores de un conjunto, de un nivel especificado a otro inferior.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Count*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Numeric_expression*  
 Opcional. Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *Include_Calc_Members*  
 Opcional. Una palabra clave que agrega miembros calculados a los resultados de exploración en profundidad.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, la **DrilldownLevelBottom** función clasifica, en orden ascendente, los elementos secundarios de cada miembro del conjunto especificado, según el valor especificado, según se ha evaluado sobre el conjunto de miembros secundarios. Si no se especifica una expresión numérica, la función ordena, de forma ascendente, los elementos secundarios de cada miembro en el conjunto especificado, según los valores de las celdas representados por el conjunto de miembros secundarios, tal y como se determinan por el contexto de la consulta. Este comportamiento es similar a las funciones BottomCount y Tail (MDX) que devuelven un conjunto de miembros en orden natural, sin ninguna ordenación.  
  
 Después de la clasificación, el **DrilldownLevelBottom** función devuelve un conjunto que contiene los miembros primarios y el número de miembros secundarios especificados en *recuento*, con el valor más bajo.  
  
 El **DrilldownLevelBottom** función es similar a la [DrilldownLevel](../mdx/drilldownlevel-mdx.md) función, pero en lugar de incluir todos los elementos secundarios de cada miembro en el nivel especificado, el  **DrilldownLevelBottom** función devuelve el número de la parte inferior de miembros secundarios.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones de obtención de detalles; consulte [propiedades XMLA compatibles &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obtener más información.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los tres elementos secundarios más bajos del nivel Product Category según la medida predeterminada. En el cubo de ejemplo de Adventure Works, los tres últimos elementos de Accessories son Tires and Tubes, Pumps y Panniers. En Management Studio, en la ventana de consulta MDX, puede ir a Products | Product Categories | Members | All Products | Accessories para ver la lista completa. Puede incrementar el argumento Count para que devuelva más miembros.  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 El ejemplo siguiente se muestra cómo utilizar el **include_calc_members** marca, que se usa para incluir miembros calculados en el nivel de detalle. La medida [Reseller Order Count] se agrega a la **DrilldownLevelBottom** instrucción para asegurarse de que los resultados se ordenen por esa medida. Para ver el miembro calculado, es necesario incrementar Count hasta 9 como mínimo.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
