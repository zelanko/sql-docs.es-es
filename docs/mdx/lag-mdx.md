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
manager: kfile
ms.openlocfilehash: 3c5479aa3ce855b554f34f72c5c86aa86eb04b9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205827"
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
  
 *Index*  
 Expresión numérica válida que especifica el número de posiciones que se van a retrasar.  
  
## <a name="remarks"></a>Comentarios  
 Las posiciones de los miembros en un nivel se determinan por el orden natural de la jerarquía de atributo. La numeración de las posiciones tiene como base cero.  
  
 Si el retraso especificado es cero, el **Lag** función devuelve el propio miembro especificado.  
  
 Si el retraso especificado es negativo, el **Lag** función devuelve un miembro subsiguiente.  
  
 `Lag(1)` es equivalente a la [PrevMember](../mdx/prevmember-mdx.md) función. `Lag(-1)` es equivalente a la [NextMember](../mdx/nextmember-mdx.md) función.  
  
 El **Lag** función es similar a la [provocar](../mdx/lead-mdx.md) funcione, salvo que el **provocar** función busca en la dirección opuesta a la **Lag** función. Es decir, `Lag(n)` es equivalente a `Lead(-n)`.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
