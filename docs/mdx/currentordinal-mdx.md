---
title: CurrentOrdinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 38ac7a3f4c966f9496f5ff9a0855960da8a38fb6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135879"
---
# <a name="currentordinal-mdx"></a>CurrentOrdinal (MDX)


  Devuelve el número de iteración actual dentro de un conjunto durante la iteración.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set_Expression.CurrentOrdinal  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 Al recorrer en iteración a través de un conjunto, como con el [Filter (MDX)](../mdx/filter-mdx.md) o [Generate (MDX)](../mdx/generate-mdx.md) funciones, la **CurrentOrdinal** función devuelve el número de iteración.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo simple muestra cómo **CurrentOrdinal** puede utilizarse con **generar** para devolver una cadena que contiene el nombre de cada elemento de un conjunto con su posición en el conjunto:  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 El uso práctico de CurrentOrdinal se limita a cálculos muy complejos. El ejemplo siguiente devuelve el número de productos del conjunto que son únicos, con el **orden** función para ordenar las tuplas no vacía antes de utilizar el **filtro** función. El **CurrentOrdinal** función se utiliza para comparar y eliminar valores equivalentes.  
  
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
    , NOT((OrdPrds.CurrentOrdinal < OrdPrds.Count   
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
          ))  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
