---
title: + Unión (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd352b95853cc5fe52857a080b6ca2e515f5c013
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68097353"
---
# <a name="union---mdx-operator-reference"></a>Union: referencia de operadores MDX


  Realiza una operación de conjunto que devuelve una unión entre dos conjuntos y elimina los miembros duplicados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>Parámetros  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="return-value"></a>Valor devuelto  
 Un conjunto que contiene los miembros de ambos conjuntos especificados.  
  
## <a name="remarks"></a>Observaciones  
 El operador **+ (Unión)** es funcionalmente equivalente a la función [Union &#40;MDX&#41;](../mdx/union-mdx.md) .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de este operador.  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
