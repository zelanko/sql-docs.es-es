---
title: Lag (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c7e95af96249b64f86bb1466283e8a1a38a32d90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905779"
---
# <a name="lag-mdx"></a>Lag (MDX)


  Devuelve el miembro que se encuentra un número especificado de posiciones por delante de un miembro especificado en el nivel del miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Lag(Index)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Ajustar*  
 Expresión numérica válida que especifica el número de posiciones que se van a retrasar.  
  
## <a name="remarks"></a>Observaciones  
 Las posiciones de los miembros en un nivel se determinan por el orden natural de la jerarquía de atributo. La numeración de las posiciones tiene como base cero.  
  
 Si el retraso especificado es cero, la función **lag** devuelve el propio miembro especificado.  
  
 Si el retraso especificado es negativo, la función **lag** devuelve un miembro subsiguiente.  
  
 `Lag(1)`es equivalente a la función [PrevMember](../mdx/prevmember-mdx.md) . `Lag(-1)`es equivalente a la función [NextMember](../mdx/nextmember-mdx.md) .  
  
 La función **lag** es similar a la función [Lead](../mdx/lead-mdx.md) , salvo que la función **Lead** busca en la dirección opuesta a la función **lag** . Es decir, `Lag(n)` es equivalente a `Lead(-n)`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor para diciembre de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(2) ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve el valor para marzo de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lag(-1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
