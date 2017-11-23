---
title: Rango (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: RANK
dev_langs: kbMDX
helpviewer_keywords: Rank function [MDX]
ms.assetid: 3cea35ed-57c4-4b47-a736-cee00275509b
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a00e9bcab64b29170ba05e9fa651d849a51b91ec
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="rank-mdx"></a>Rank (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, la **rango** función determina el rango basado en uno de la tupla especificada mediante la evaluación de la expresión numérica especificada en la tupla. Si se especifica una expresión numérica, la **rango** función asigna el mismo rango a tuplas con valores duplicados en el conjunto. Esta asignación del mismo rango a valores duplicados afecta a los rangos de las tuplas subsiguientes del conjunto. Por ejemplo, un conjunto consta de las siguientes tuplas, `{(a,b), (e,f), (c,d)}`. La tupla `(a,b)` tiene el mismo valor que la tupla `(c,d)`. Si la tupla `(a,b)` tiene el rango 1, `(a,b)` y `(c,d)` tendrían el rango 1. Sin embargo, la tupla `(e,f)` tendría el rango 3. No podría haber ninguna tupla en este conjunto con el rango 2.  
  
 Si no se especifica una expresión numérica, la **rango** función devuelve la posición ordinal basado en uno de la tupla especificada.  
  
 El **rango** función no ordena el conjunto.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se devuelve el conjunto de tuplas que contiene clientes y fechas de compra mediante el uso de la **filtro**, **NonEmpty**, **elemento**, y **rango** funciones para encontrar la última fecha en que cada cliente realizó una compra.  
  
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
  
 En el ejemplo siguiente se usa el **orden** función, en lugar de la **rango** función, para clasificar los miembros de la jerarquía City según la medida Reseller Sales Amount y mostrarlos en un orden de rango. Mediante el uso de la **orden** funcionar al primer pedido el conjunto de miembros de la jerarquía City, la ordenación se realiza una sola vez y, a continuación, seguida de una exploración lineal antes de que se presentan en orden alfabético.  
  
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
 [Orden &#40; MDX &#41;](../mdx/order-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
