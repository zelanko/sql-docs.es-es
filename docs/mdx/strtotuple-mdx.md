---
title: StrToTuple (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 232d1e94892165430867ec5217f8c87ccd625b48
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036714"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  Devuelve la tupla especificada por una cadena con formato de expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Specification*  
 Expresión de cadena válida que especifica, directa o indirectamente, una tupla.  
  
## <a name="remarks"></a>Observaciones  
 La función **StrToTuple** devuelve el conjunto especificado. La función **StrToTuple** se usa normalmente con funciones definidas por el usuario para devolver una especificación de tupla de una función externa a una instrucción MDX.  
  
-   Cuando se utiliza la marca CONSTRAINED, la especificación de tupla debe contener nombres de miembro calificados o no calificados. Esta marca se utiliza para reducir el riesgo de ataques por inyección de código a través de la cadena especificada. Si se proporciona una cadena que no se resuelve directamente en nombres de miembro calificados o no calificados, aparece el siguiente error: "Se infringieron las restricciones impuestas por la marca CONSTRAINED en la función STRTOTUPLE."  
  
-   Cuando no se utiliza la marca CONSTRAINED, la tupla especificada se puede resolver en una expresión MDX válida que devuelve una tupla.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la medida Reseller Sales Amount del miembro Bayern para el año natural 2004. La especificación de la tupla que se proporciona contiene una expresión de tupla MDX válida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve la medida Reseller Sales Amount del miembro Bayern para el año natural 2004. La especificación de tupla que se proporciona contiene nombres de miembro calificados, tal como requiere la marca CONSTRAINED.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve la medida Reseller Sales Amount del miembro Bayern para el año natural 2004. La especificación de la tupla que se proporciona contiene una expresión de tupla MDX válida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve un error debido a la marca CONSTRAINED. Mientras que la especificación de tupla proporcionada contiene una expresión de tupla MDX válida, la marca CONSTRAINED necesita nombres de miembro calificados o no calificados en la especificación de tupla.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
