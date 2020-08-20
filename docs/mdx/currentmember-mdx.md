---
description: CurrentMember (MDX)
title: CurrentMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e04dd1146bc55d8d68475770a9077fc8d962b56d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471877"
---
# <a name="currentmember-mdx"></a>CurrentMember (MDX)


  Devuelve el miembro actual de una jerarquía especificada durante la iteración.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Hierarchy_Expression.CurrentMember  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
## <a name="remarks"></a>Observaciones  
 En cada paso de una iteración en un conjunto de miembros de jerarquía, el miembro con el que se está trabajando es el miembro actual. La función **CurrentMember** devuelve ese miembro.  
  
> [!IMPORTANT]  
>  Cuando una dimensión contiene solo una única jerarquía visible, se puede hacer referencia a la jerarquía por el nombre de la dimensión o por el nombre de la jerarquía, dado que el nombre de la dimensión se resuelve en su única jerarquía visible. Por ejemplo, `Measures.CurrentMember` es una expresión MDX válida debido a que se resuelve en la única jerarquía de la dimensión Measures.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra cómo se puede usar **CurrentMember** para buscar el miembro actual de las jerarquías en el eje de columnas, filas y segmentos:  
  
 `WITH MEMBER MEASURES.CURRENTDATE AS`  
  
 `[Date].[Calendar].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTPRODUCT AS`  
  
 `[Product].[Product Categories].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTMEASURE AS`  
  
 `MEASURES.CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.CURRENTCUSTOMER AS`  
  
 `[Customer].[Customer Geography].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `[Product].[Product Categories].[Category].MEMBERS`  
  
 `*`  
  
 `{MEASURES.CURRENTDATE, MEASURES.CURRENTPRODUCT,MEASURES.CURRENTMEASURE, MEASURES.CURRENTCUSTOMER}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Customer].[Customer Geography].[Country].&[Australia])`  
  
 El miembro actual cambia en una jerarquía que se utiliza en un eje en una consulta. Por lo tanto, el miembro actual de otras jerarquías de la misma dimensión que no se utilizan en un eje también puede cambiar; Este comportamiento se denomina "auto-EXISTS" y se pueden encontrar más detalles en [conceptos clave de MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services). Por ejemplo, la consulta siguiente muestra cómo el miembro actual en la jerarquía Calendar Year de la dimensión Date cambia con el miembro actual en la jerarquía Calendar, cuando el último se muestra en el eje de filas:  
  
 `WITH MEMBER MEASURES.CURRENTYEAR AS`  
  
 `[Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `SELECT`  
  
 `{MEASURES.CURRENTYEAR}`  
  
 `ON 0,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 **CurrentMember** es muy importante para realizar cálculos que tengan en cuenta el contexto de la consulta en la que se usan. En el ejemplo siguiente se devuelve la cantidad de pedido de cada producto y el porcentaje de cantidades de pedido por categoría y modelo del cubo **Adventure Works** . La función **CurrentMember** identifica el producto cuya cantidad de pedido se va a usar durante el cálculo.  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty  
(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
