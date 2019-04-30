---
title: Rank (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d234f02c8dfcd36073059210c1999cb95f5ab0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200666"
---
# <a name="rank-mdx"></a>Rank (MDX)


  Devuelve el intervalo con base uno de una tupla especificada en un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Rank(Tuple_Expression, Set_Expression [ ,Numeric Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, la **rango** función determina el rango basado en uno de la tupla especificada mediante la evaluación de la expresión numérica especificada con la tupla. Si se especifica una expresión numérica, la **rango** función asigna el mismo rango a las tuplas con valores duplicados en el conjunto. Esta asignación del mismo rango a valores duplicados afecta a los rangos de las tuplas subsiguientes del conjunto. Por ejemplo, un conjunto consta de las siguientes tuplas, `{(a,b), (e,f), (c,d)}`. La tupla `(a,b)` tiene el mismo valor que la tupla `(c,d)`. Si la tupla `(a,b)` tiene el rango 1, `(a,b)` y `(c,d)` tendrían el rango 1. Sin embargo, la tupla `(e,f)` tendría el rango 3. No podría haber ninguna tupla en este conjunto con el rango 2.  
  
 Si no se especifica una expresión numérica, la **rango** función devuelve la posición ordinal basado en uno de la tupla especificada.  
  
 El **rango** función no ordena el conjunto.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el conjunto de tuplas que contiene clientes y fechas de compra mediante el uso de la **filtro**, **NonEmpty**, **elemento**, y **rango** funciones para buscar la última fecha en que cada cliente realizó una compra.  
  
```  
WITH SET MYROWS AS FILTER  
   (NONEMPTY  
      ([Customer].[Customer Geography].MEMBERS  
         * [Date].[Date].[Date].MEMBERS  
         , [Measures].[Internet Sales Amount]  
      ) AS MYSET  
   , NOT(MYSET.CURRENT.ITEM(0)  
      IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))  
   )  
SELECT [Measures].[Internet Sales Amount] ON 0,  
MYROWS ON 1  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se usa el **orden** función, en lugar de **rango** función, para clasificar los miembros de la jerarquía City, según la medida Reseller Sales Amount y, a continuación, se muestra en el orden de rango. Mediante el uso de la **orden** función en primer lugar el conjunto de miembros de la jerarquía City, la ordenación se realiza solo una vez y, a continuación, seguida de una exploración lineal antes de que se presentan en orden alfabético.  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Order &#40;MDX&#41;](../mdx/order-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
