---
title: Primario (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9449c81e9f8e8de0c21d96062337e91b2f56398d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037197"
---
# <a name="parent-mdx"></a>Parent (MDX)


  Devuelve el elemento primario de un miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Parent   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 La función **Parent** devuelve el miembro primario del miembro especificado.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes devuelven el elemento primario del miembro 1 de julio de 2001. El primer ejemplo especifica este miembro en el contexto de la jerarquía de atributo Date y devuelve el miembro All Periods.  
  
```  
SELECT [Date].[Date].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente especifica el miembro 1 de julio de 2001 en el contexto de la jerarquía Calendar.  
  
```  
SELECT [Date].[Calendar].[July 1, 2001].Parent ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
