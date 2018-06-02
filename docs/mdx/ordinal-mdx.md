---
title: Ordinal (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61c5c3c4bbb2f04f1ebb9743e18eb8088632eab0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581267"
---
# <a name="ordinal-mdx"></a>Ordinal (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor ordinal (con base cero) asociado a un nivel.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level_Expression.Ordinal   
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Notas  
 El **Ordinal** función se utiliza habitualmente junto con el **IIF** y **CurrentMember** funciones para mostrar condicionalmente distintos valores en diferentes niveles de jerarquía, basándose en la posición ordinal de cada celda específica en el resultado de la consulta. Por ejemplo, puede usar el **Ordinal** función para realizar cálculos en ciertos niveles y mostrará el valor predeterminado "N/A" en otros niveles.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el número ordinal del nivel Calendar Quarter de la jerarquía Calendar.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
