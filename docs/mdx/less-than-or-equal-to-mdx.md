---
title: '&lt;= (Menor o igual que) (MDX) | Documentos de Microsoft'
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2904598ecb9019660e1751dd585714d80d874b02
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579067"
---
# <a name="lt-less-than-or-equal-to-mdx"></a>&lt;= (Menor o igual que) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
-   t**rue** si ambos parámetros son distintos de null y el primer parámetro tiene un valor que sea menor o igual que el valor del segundo parámetro.  
  
-   f**alse** si ambos parámetros son distintos de null y el primer parámetro tiene un valor que mayor que el valor del segundo parámetro.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
