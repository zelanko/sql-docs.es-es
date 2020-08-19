---
description: '&lt;= (Menor o igual que) (MDX)'
title: '&lt;= (Menor o igual que) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c800f39898127d7e7b7fe9b0bef8df46040d834
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429897"
---
# <a name="lt-less-than-or-equal-to-mdx"></a>&lt;= (Menor o igual que) (MDX)


  Realiza una operación de comparación que determina si el valor de una expresión multidimensional (MDX) es inferior o igual al valor de otra expresión MDX.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MDX_Expression <= MDX_Expression  
```  
  
#### <a name="parameters"></a>Parámetros  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano basado en las condiciones siguientes:  
  
-   t**Rue** si ambos parámetros son no NULL y el primer parámetro tiene un valor que es menor o igual que el valor del segundo parámetro.  
  
-   f**alse** si ambos parámetros son no NULL y el primer parámetro tiene un valor que es mayor que el valor del segundo parámetro.  
  
-   valor NULL si uno de los parámetros (o ambos) se evalúa en un valor NULL.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is less than or equal to 30%.  
With Member [Measures].[LowGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] <= .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[LowGPM])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
