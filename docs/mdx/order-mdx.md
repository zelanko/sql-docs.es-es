---
title: Order (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d540b299fd08aa78576b19040a4cfafb9046ae7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055682"
---
# <a name="order-mdx"></a>Order (MDX)


  Organiza los miembros de un conjunto especificado; opcionalmente preservando o rompiendo la jerarquía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_Expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número expresado como una cadena.  
  
## <a name="remarks"></a>Comentarios  
 El **orden** función pueden ser jerárquica (como se especifica mediante el uso de la **ASC** o **DESC** marca) o no jerárquica (como se especifica mediante el uso de la **BASC**  o **BDESC** marca; el **B** "jerarquía de salto" es el acrónimo). Si **ASC** o **DESC** se especifica, el **orden** función primero organiza los miembros según su posición en la jerarquía y, a continuación, ordena cada nivel. Si **BASC** o **BDESC** se especifica, el **orden** función organiza los miembros del conjunto sin tener en cuenta la jerarquía. Se especifica ninguna marca, **ASC** es el valor predeterminado.  
  
 Si el **orden** función se utiliza con un conjunto donde dos o más jerarquías son ejecutar la función Crossjoin y el **DESC** marca se utiliza, solo los miembros de la última jerarquía del conjunto se ordenan. Este es un cambio con respecto a Analysis Services 2000 donde todas las jerarquías del conjunto estaban ordenadas.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve, desde el **Adventure Works** del cubo, el número de pedidos del distribuidor para todos los trimestres naturales de la jerarquía Calendar de la dimensión Date. El **orden** función vuelve a ordenar el conjunto para el eje ROWS. El **orden** función ordena el conjunto por `[Reseller Order Count]` en orden jerárquico descendente según lo determinado por la `[Calendar]` jerarquía.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Observe cómo en este ejemplo, cuando el **DESC** marca se cambia a **BDESC**, se rompe la jerarquía y la lista de trimestres naturales se devuelve sin tener en cuenta para la jerarquía:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 El ejemplo siguiente devuelve la medida Reseller Sales de las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. El **subconjunto** función se utiliza para devolver solo las 5 primeras tuplas del conjunto una vez que el resultado se ordena mediante la **orden** función.  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 En el ejemplo siguiente se usa el **rango** función para clasificar los miembros de la jerarquía City, según la medida Reseller Sales Amount y, a continuación, se muestra en el orden de rango. Mediante el uso de la **orden** función en primer lugar el conjunto de miembros de la jerarquía City, la ordenación se realiza solo una vez y, a continuación, seguida de una exploración lineal antes de que se presentan en orden alfabético.  
  
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
  
 El ejemplo siguiente devuelve el número de productos del conjunto que son únicos, con el **orden** función para ordenar las tuplas no vacía antes de utilizar el **filtro** función. El **CurrentOrdinal** función se utiliza para comparar y eliminar valores equivalentes.  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 Para comprender cómo la **DESC** marca funciona con conjuntos de tuplas, considere primero los resultados de la consulta siguiente:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 En el eje de filas puede ver que los Sales Territory Groups se han clasificado en orden descendente por Tax Amount, como sigue: North America, Europe, Pacific, NA. Ahora vea lo que sucede si nos combinación cruzada del conjunto de Sales Territory Groups con el conjunto de Product Subcategories y aplicar el **orden** funcione de la misma manera, como se indica a continuación:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Mientras que el conjunto de Product Subcategories se ha ordenado en orden jerárquico descendente los Sales Territory Groups ahora no están ordenados y aparecen en el orden en que aparecen en la jerarquía: Europa, NA, Norteamérica y Pacífico. Esto se debe a que solo está ordenada la última jerarquía del conjunto de tuplas, Product Subcategories. Para reproducir el comportamiento de Analysis Services 2000, utilice una serie de anidado **generar** funciones para ordenar cada conjunto antes de ejecutar la función Crossjoin, por ejemplo:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
