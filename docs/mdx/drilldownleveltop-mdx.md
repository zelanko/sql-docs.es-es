---
title: DrilldownLevelTop (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d6532998f65625bf3dacd11de2949a3478ba6ea
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146220"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  Aumenta el detalle de los miembros superiores de un conjunto, de un nivel especificado a otro inferior.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Count*  
 Expresión numérica válida que especifica el número de tuplas que serán devueltas.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *Include_Calc_Members*  
 Una palabra clave para agregar miembros calculados a los resultados de exploración en profundidad.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, la **DrilldownLevelTop** función clasifica, en orden descendente, los elementos secundarios de cada miembro del conjunto especificado de acuerdo con el valor de la expresión numérica, según se ha evaluado sobre el conjunto de secundarios miembros. Si no se especifica una expresión numérica, la función clasifica, en orden descendente, los elementos secundarios de cada miembro del conjunto especificado de acuerdo con los valores de las celdas representadas por el conjunto de miembros secundarios, según determine el contexto de consulta.  
  
 Después de la clasificación, el **DrilldownLevelTop** función devuelve un conjunto que contiene los miembros primarios y el número de miembros secundarios especificados en *recuento,* con el valor más alto.  
  
 El **DrilldownLevelTop** función es similar a la [DrilldownLevel](../mdx/drilldownlevel-mdx.md) función, pero en lugar de incluir todos los elementos secundarios de cada miembro en el nivel especificado, el **DrilldownLevelTop** función devuelve el número más alto de miembros secundarios.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones de obtención de detalles; consulte [propiedades XMLA compatibles &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obtener más información.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los tres primeros elementos secundarios del nivel Product Category según la medida predeterminada. En el cubo de ejemplo de Adventure Works, los tres elementos secundarios principales de Accessories son Bike Racks, Bike Stands y Bottles and Cages. En Management Studio, en la ventana de consulta MDX, puede ir a Products | Product Categories | Members | All Products | Accessories para ver la lista completa. Puede incrementar el argumento Count para que devuelva más miembros.  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 El ejemplo siguiente se muestra cómo utilizar el **include_calc_members** marca, que se usa para incluir miembros calculados en el nivel de detalle. La medida [Reseller Order Count] se incluye en el **DrilldownLevelTop** instrucción para asegurarse de que los valores devueltos se ordenan por esa medida.  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
