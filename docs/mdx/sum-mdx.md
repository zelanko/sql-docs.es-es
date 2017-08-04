---
title: SUM (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUM
dev_langs:
- kbMDX
helpviewer_keywords:
- Sum function [MDX]
ms.assetid: 6c3db1e3-2c02-49f2-a0bf-cab0fb78c622
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9825bd3230e2cc9e962d059e87a31f1e569ec8b8
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="sum-mdx"></a>Sum (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la suma de una expresión numérica evaluada sobre un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Sum( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Una expresión de conjunto de MDX (Expresiones multidimensionales) válida.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica una expresión numérica, ésta se evalúa en el conjunto y, a continuación, se suma. Si no se especifica una expresión numérica, el conjunto especificado se evalúa en el contexto actual de los miembros del conjunto y, a continuación, se suma. Si la función SUM se aplica a una expresión no numérica, los resultados quedarán sin definir.  
  
> [!NOTE]  
>  Analysis Services omite los valores nulos al calcular la suma de un conjunto de números.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la suma de Reseller Sales Amounts para todos los miembros de la jerarquía de atributo Product.Category para los años 2001 y 2002.  
  
```  
WITH MEMBER Measures.x AS SUM  
   ( { [Date].[Calendar Year].&[2001]  
         , [Date].[Calendar Year].&[2002] }  
      , [Measures].[Reseller Sales Amount]  
    )  
SELECT Measures.x ON 0  
,[Product].[Category].Members ON 1  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve la suma de los costos de flete correspondientes a las ventas por Internet del mes de julio de 2002 hasta el día 20 de julio.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se utiliza la palabra clave WITH MEMBER y **suma** función para definir un miembro calculado en la dimensión Measures que contiene la suma de la medida Reseller Sales Amount para los miembros Canada y United States de la jerarquía de atributo Country de la dimensión Geography.  
  
```  
WITH MEMBER Measures.NorthAmerica AS SUM   
      (  
         {[Geography].[Country].&[Canada]  
            , [Geography].[Country].&[United States]}  
       ,[Measures].[Reseller Sales Amount]  
      )  
SELECT {[Measures].[NorthAmerica]} ON 0,  
[Product].[Category].members ON 1  
FROM [Adventure Works]  
```  
  
 A menudo, el **suma** función se utiliza con la **CURRENTMEMBER** función o las funciones como **YTD** que devuelve un conjunto que varía según el miembro actual de una jerarquía. Por ejemplo, la siguiente consulta devuelve la suma de la medida Internet Sales Amount para todas las fechas desde principio del año natural hasta la fecha mostrada en el eje de filas:  
  
 `WITH MEMBER MEASURES.YTDSUM AS`  
  
 `SUM(YTD(), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount], MEASURES.YTDSUM} ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

