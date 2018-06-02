---
title: NextMember (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 506151f7f88653fe260cadd09354705b3e5f98d9
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580367"
---
# <a name="nextmember-mdx"></a>NextMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el siguiente miembro del nivel que contiene un miembro especificado  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.NextMember   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 El **NextMember** función devuelve el miembro siguiente, en el mismo nivel, que contiene el miembro especificado.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve el miembro August 2001 como el siguiente al miembro July 2001.  
  
```  
SELECT [Date].[Calendar].[Month].[July 2001].NextMember ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
