---
description: CurrentOrdinal (MDX)
title: CurrentOrdinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68119266fd9460a28e036914fce036ec165e553a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413161"
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
  
## <a name="remarks"></a>Observaciones  
 Al recorrer en iteración un conjunto, como con las funciones de [filtro (MDX)](../mdx/filter-mdx.md) o [generar (MDX)](../mdx/generate-mdx.md) , la función **CurrentOrdinal** devuelve el número de iteración.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo simple se muestra cómo se puede usar **CurrentOrdinal** con **Generate** para devolver una cadena que contiene el nombre de cada elemento de un conjunto junto con su posición en el conjunto:  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 El uso práctico de CurrentOrdinal se limita a cálculos muy complejos. En el ejemplo siguiente se devuelve el número de productos del conjunto que son únicos, usando la función **Order** para ordenar las tuplas no vacías antes de utilizar la función de **filtro** . La función **CurrentOrdinal** se usa para comparar y eliminar las relaciones.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
