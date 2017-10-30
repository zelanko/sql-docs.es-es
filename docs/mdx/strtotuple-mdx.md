---
title: StrToTuple (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRTOTUPLE
dev_langs:
- kbMDX
helpviewer_keywords:
- StrToTuple function
ms.assetid: e162cc01-cddd-4654-baab-d73abdc33b80
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2ca9d105bf04c91fd2c65bea74f92a0d0ef1edd
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la tupla especificada por una cadena con formato de Expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Tuple_Specification*  
 Expresión de cadena válida que especifica, directa o indirectamente, una tupla.  
  
## <a name="remarks"></a>Comentarios  
 El **StrToTuple** función devuelve el conjunto especificado. El **StrToTuple** función normalmente se utiliza con funciones definidas por el usuario para devolver una especificación de tupla desde una función externa a una instrucción MDX.  
  
-   Cuando se utiliza la marca CONSTRAINED, la especificación de tupla debe contener nombres de miembro calificados o no calificados. Esta marca se utiliza para reducir el riesgo de ataques por inyección de código a través de la cadena especificada. Si se proporciona una cadena que no se resuelve directamente en nombres de miembro calificados o no calificados, aparece el siguiente error: "Se infringieron las restricciones impuestas por la marca CONSTRAINED en la función STRTOTUPLE."  
  
-   Cuando no se utiliza la marca CONSTRAINED, la tupla especificada se puede resolver en una expresión MDX válida que devuelve una tupla.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la medida Reseller Sales Amount del miembro Bayern para el año natural 2004. La especificación de la tupla que se proporciona contiene una expresión de tupla MDX válida.  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve la medida Reseller Sales Amount del miembro Bayern para el año natural 2004. La especificación de tupla que se proporciona contiene nombres de miembro calificados, según sea necesario mediante la marca CONSTRAINED.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

