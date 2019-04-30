---
title: '* (Combinaciones cruzadas) (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 132b237fd8baa9c50dc254b02d90ed95d7159a0c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63249620"
---
# <a name="crossjoin----mdx-operator-reference"></a>Crossjoin - referencia de operadores de MDX


  Realiza una operación de conjunto que devuelve el producto cruzado de dos conjuntos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set_Expression * Set_Expression  
```  
  
## <a name="parameter"></a>Parámetro  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="return-value"></a>Valor devuelto  
 Conjunto que contiene el producto cruzado de ambos parámetros especificados.  
  
## <a name="remarks"></a>Comentarios  
 El  **\* (combinaciones cruzadas)** operador es funcionalmente equivalente a la [Crossjoin](../mdx/crossjoin-mdx.md) función.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
-- This query returns the gross profit margin for product types  
-- and reseller types crossjoined by year.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members *  
    [Reseller].[Reseller Type].Children ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
