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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
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
  
## <a name="remarks"></a>Observaciones  
 La función **Order** puede ser jerárquica (como se especifica mediante el uso de la marca **ASC** o **DESC** ) o no jerárquica (como se especifica mediante el uso de la marca **BASC** o **BDESC** ; **B** representa la "jerarquía de interrupción"). Si se especifica **ASC** o **DESC** , la función **Order** organiza primero los miembros según su posición en la jerarquía y, a continuación, ordena cada nivel. Si se especifica **BASC** o **BDESC** , la función **Order** organiza los miembros del conjunto sin tener en cuenta la jerarquía. En el caso de que no se especifique ninguna marca, **ASC** es el valor predeterminado.  
  
 Si la función **Order** se usa con un conjunto en el que dos o más jerarquías son Unidos y se usa la marca **DESC** , solo se ordenan los miembros de la última jerarquía del conjunto. Este es un cambio con respecto a Analysis Services 2000 donde todas las jerarquías del conjunto estaban ordenadas.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve, del cubo **Adventure Works** , el número de pedidos de distribuidor de todos los trimestres naturales de la jerarquía Calendar de la dimensión Date. La función **Order** reordena el conjunto para el eje Rows. La función **Order** ordena el conjunto `[Reseller Order Count]` en orden jerárquico descendente según lo determinado por la `[Calendar]` jerarquía.  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Observe que en este ejemplo, cuando se cambia la marca **DESC** a **BDESC**, la jerarquía se rompe y se devuelve la lista de trimestres naturales sin tener en cuenta la jerarquía:  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 El ejemplo siguiente devuelve la medida Reseller Sales de las cinco subcategorías de productos más vendidos, independientemente de su jerarquía, de acuerdo con Reseller Gross Profit. La función **subset** se utiliza para devolver solo las 5 primeras tuplas del conjunto después de que el resultado se ordene mediante la función **Order** .  
  
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
  
 En el ejemplo siguiente se usa la función **Rank** para clasificar los miembros de la jerarquía City, en función de la medida reseller sales amount y, a continuación, se muestran en el orden ordenado. Mediante el uso de la función **Order** para ordenar por primera vez el conjunto de miembros de la jerarquía City, la ordenación se realiza una sola vez y, después, sigue un examen lineal antes de que se presente en el criterio de ordenación.  
  
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
  
 En el ejemplo siguiente se devuelve el número de productos del conjunto que son únicos, usando la función **Order** para ordenar las tuplas no vacías antes de utilizar la función de **filtro** . La función **CurrentOrdinal** se usa para comparar y eliminar las relaciones.  
  
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
  
 Para entender cómo funciona la marca **DESC** con conjuntos de tuplas, considere primero los resultados de la siguiente consulta:  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 En el eje de las filas puede ver que los Sales Territory Groups se han clasificado en orden descendente por Tax Amount, como sigue: North America, Europa, Pacific, NA. Ahora vea lo que ocurre si se crea un conjunto de grupos de territorio de ventas con el conjunto de subcategorías de productos y se aplica la función **Order** de la misma manera, como se indica a continuación:  
  
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
  
 Aunque el conjunto de Product Subcategories se ha clasificado ahora en orden jerárquico descendente, los Sales Territory Groups están ordenados y ahora aparecen en el mismo orden que en la jerarquía: Europe, NA, North America y Pacific. Esto se debe a que solo está ordenada la última jerarquía del conjunto de tuplas, Product Subcategories. Para reproducir el comportamiento de Analysis Services 2000, utilice una serie de funciones de **generación** anidadas para ordenar cada conjunto antes de que se Unidos, por ejemplo:  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
