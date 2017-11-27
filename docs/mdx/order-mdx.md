---
title: Orden (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORDER
dev_langs:
- kbMDX
helpviewer_keywords:
- Order function
ms.assetid: 84acff52-2443-4424-a09e-694e6f14c109
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 98037f9c56523e05a1d3af44078bf8da51cd53e5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="order-mdx"></a>Order (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
 *String_Expression*  
 Expresión de cadena válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número expresado como una cadena.  
  
## <a name="remarks"></a>Comentarios  
 El **orden** función puede ser jerárquica (como se especifica mediante el uso de la **ASC** o **DESC** marca) o no jerárquica (como se especifica mediante el uso de la **BASC** o **BDESC** marca; el **B** es el acrónimo "jerarquía de salto"). Si **ASC** o **DESC** se especifica, el **orden** función primero organiza los miembros según su posición en la jerarquía y, a continuación, ordena cada nivel. Si **BASC** o **BDESC** se especifica, el **orden** función organiza los miembros del conjunto sin tener en cuenta la jerarquía. Se especifica ninguna marca, **ASC** es el valor predeterminado.  
  
 Si el **orden** función se utiliza con un conjunto donde dos o más jerarquías están Unidos y la **DESC** marca se utiliza, solo los miembros de la última jerarquía del conjunto se ordenan. Este es un cambio con respecto a Analysis Services 2000 donde todas las jerarquías del conjunto estaban ordenadas.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve, desde el **Adventure Works** del cubo, el número de pedidos de distribuidores para todos los trimestres naturales de la jerarquía de calendario en la dimensión Date. El **orden** función vuelve a ordenar el conjunto para el eje de filas. El **orden** función ordena el conjunto por `[Reseller Order Count]` en orden jerárquico descendente según lo determinado por la `[Calendar]` jerarquía.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Observe cómo en este ejemplo, cuando la **DESC** marca se cambia a **BDESC**, se interrumpe la jerarquía y la lista de trimestres naturales se devuelve sin tener en cuenta para la jerarquía:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 El ejemplo siguiente devuelve la medida Reseller Sales de las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. El **subconjunto** función se utiliza para devolver solo las 5 primeras tuplas del conjunto después de que el resultado se ordena mediante la **orden** función.  
  
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
  
 En el ejemplo siguiente se usa el **rango** función para clasificar los miembros de la jerarquía City, en función de la medida Reseller Sales Amount y mostrarlos en un orden de rango. Mediante el uso de la **orden** funcionar al primer pedido el conjunto de miembros de la jerarquía City, la ordenación se realiza una sola vez y, a continuación, seguida de una exploración lineal antes de que se presentan en orden alfabético.  
  
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
  
 El ejemplo siguiente devuelve el número de productos en el conjunto que son únicos, con el **orden** función para ordenar las tuplas de no vacío antes de utilizar el **filtro** función. El **CurrentOrdinal** función se utiliza para comparar y eliminar valores equivalentes.  
  
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
  
 En el eje de las filas puede ver que los Sales Territory Groups se han clasificado en orden descendente por Tax Amount, como sigue: North America, Europe, Pacific, NA. Ahora vea lo que ocurre si se combinación cruzada del conjunto de Sales Territory Groups con el conjunto de subcategorías de productos y aplicar el **orden** función de la misma manera, como se indica a continuación:  
  
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
  
 Aunque el conjunto de Product Subcategories se ha clasificado ahora en orden jerárquico descendente, los Sales Territory Groups están ordenados y ahora aparecen en el mismo orden que en la jerarquía: Europe, NA, North America y Pacific. Esto se debe a que solo está ordenada la última jerarquía del conjunto de tuplas, Product Subcategories. Para reproducir el comportamiento de Analysis Services 2000, use una serie de anidar **generar** funciones para ordenar cada conjunto antes de ejecutar la función Crossjoin, por ejemplo:  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

