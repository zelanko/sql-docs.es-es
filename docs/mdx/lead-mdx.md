---
title: Provocar (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e9faf5d0f7b549887c6aa4a12e4c502c2663ce3
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578997"
---
# <a name="lead-mdx"></a>Lead (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el miembro que se encuentra un número especificado de posiciones por detrás de un miembro especificado en el nivel del miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Lead( Index )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Index*  
 Expresión numérica válida que especifica el número de posiciones de los miembros.  
  
## <a name="remarks"></a>Notas  
 Las posiciones de los miembros en un nivel se determinan por el orden natural de la jerarquía de atributo. La numeración de las posiciones tiene como base cero.  
  
 Si la posición inicial especificada es cero (0), el **provocar** función devuelve el miembro especificado.  
  
 Si la posición inicial especificada es negativa, el **provocar** función devuelve un miembro anterior.  
  
 `Lead(1)` es equivalente a la [NextMember](../mdx/nextmember-mdx.md) función. `Lead(-1)` es equivalente a la [PrevMember](../mdx/prevmember-mdx.md) función.  
  
 El **provocar** función es similar a la [Lag](../mdx/lag-mdx.md) funcione, salvo que la **Lag** función busca en la dirección opuesta a la **provocar** función. Es decir, `Lead(n)` es equivalente a `Lag(-n)`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el valor para diciembre de 2001:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(-2) ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve el valor para marzo de 2002:  
  
```  
SELECT [Date].[Fiscal].[Month].[February 2002].Lead(1) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
