---
title: Ordinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b22cc6d5a609f8e1f585ccc1229e0e1cd67e1796
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055637"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)


  Devuelve el valor ordinal (con base cero) asociado a un nivel.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Comentarios  
 El **Ordinal** función se utiliza con frecuencia junto con el **IIF** y **CurrentMember** funciones para mostrar condicionalmente distintos valores en diferentes niveles de jerarquía, según la posición ordinal de cada celda específica en el resultado de la consulta. Por ejemplo, puede usar el **Ordinal** función para realizar cálculos en ciertos niveles y mostrar su valor predeterminado "N/A" en otros niveles.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el número ordinal del nivel Calendar Quarter de la jerarquía Calendar.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
