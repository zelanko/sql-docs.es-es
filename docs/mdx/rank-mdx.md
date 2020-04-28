---
title: Rango (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1081cacd0676f4eb0512780e9ddc7641edb99ca1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68037070"
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
  
## <a name="remarks"></a>Observaciones  
 Si se especifica una expresión numérica, la función **Rank** determina el rango basado en uno de la tupla especificada evaluando la expresión numérica especificada en la tupla. Si se especifica una expresión numérica, la función **Rank** asigna el mismo rango a las tuplas con valores duplicados en el conjunto. Esta asignación del mismo rango a valores duplicados afecta a los rangos de las tuplas subsiguientes del conjunto. Por ejemplo, un conjunto consta de las siguientes tuplas, `{(a,b), (e,f), (c,d)}`. La tupla `(a,b)` tiene el mismo valor que la tupla `(c,d)`. Si la tupla `(a,b)` tiene el rango 1, `(a,b)` y `(c,d)` tendrían el rango 1. Sin embargo, la tupla `(e,f)` tendría el rango 3. No podría haber ninguna tupla en este conjunto con el rango 2.  
  
 Si no se especifica una expresión numérica, la función **Rank** devuelve la posición ordinal basada en uno de la tupla especificada.  
  
 La función **Rank** no ordena el conjunto.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve el conjunto de tuplas que contienen los clientes y las fechas de compra mediante las funciones **Filter**, **NonEmpty**, **Item**y **Rank** para buscar la última fecha en la que cada cliente realizó una compra.  
  
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
  
 En el ejemplo siguiente se usa la función **Order** , en lugar de la función **Rank** , para clasificar los miembros de la jerarquía City según la medida reseller sales amount y, a continuación, se muestran en el orden clasificado. Mediante el uso de la función **Order** para ordenar por primera vez el conjunto de miembros de la jerarquía City, la ordenación se realiza una sola vez y, después, sigue un examen lineal antes de que se presente en el criterio de ordenación.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Orden &#40;MDX&#41;](../mdx/order-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
