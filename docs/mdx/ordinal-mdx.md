---
description: Ordinal (MDX)
title: Ordinal (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 74811da22f8c73536749acad41dfbe859b00eeea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471737"
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
  
## <a name="remarks"></a>Observaciones  
 La función **ordinal** se usa con frecuencia junto con las funciones **IIf** y **CurrentMember** para mostrar condicionalmente diferentes valores en distintos niveles de jerarquía, en función de la posición ordinal de cada celda específica en el resultado de la consulta. Por ejemplo, puede usar la función **ordinal** para realizar cálculos en determinados niveles y mostrar un valor predeterminado de "N/a" en otros niveles.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el número ordinal del nivel Calendar Quarter de la jerarquía Calendar.  
  
```  
WITH MEMBER Measures.x AS [Date].[Calendar].[Calendar Quarter].Ordinal  
SELECT Measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
