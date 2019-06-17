---
title: NextMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4535b837d81db10f41f1445a7051678ce4fdd688
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63277854"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)


  Devuelve el siguiente miembro del nivel que contiene un miembro especificado  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **NextMember** función devuelve el miembro siguiente, en el mismo nivel, que contiene el miembro especificado.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el miembro August 2001 como el siguiente al miembro July 2001.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
