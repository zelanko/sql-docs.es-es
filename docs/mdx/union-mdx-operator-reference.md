---
title: + (Unión) (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bebcf04c248251e2272d4135c129c519f48f7405
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34582447"
---
# <a name="union---mdx-operator-reference"></a>Unión - referencia de operadores MDX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Notas  
 El **+ (unión)** operador es funcionalmente equivalente a la [unión &#40;MDX&#41; ](../mdx/union-mdx.md) (función).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
