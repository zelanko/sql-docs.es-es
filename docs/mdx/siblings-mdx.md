---
title: Elementos del mismo nivel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9d8ba2dd26575ebd41f4a6c275a2668b1421dee6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68036947"
---
# <a name="siblings-mdx"></a>Siblings (MDX)


  Devuelve los miembros del mismo nivel que un miembro especificado, incluyendo el propio miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Siblings   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
### <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la medida predeterminada de los miembros del mismo nivel que marzo de 2003, que son enero de 2003 y febrero de 2003, incluido marzo de 2003.  
  
```  
SELECT [Date].[Calendar].[Month].[March 2003].Siblings ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
