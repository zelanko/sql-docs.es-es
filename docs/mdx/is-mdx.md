---
title: ES (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaf4151d8291ccd4249892c6ef8fce8a3d280f6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905980"
---
# <a name="is-mdx"></a>IS (MDX)


  Realiza una comparación lógica entre dos expresiones de objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Expression1*  
 Expresión de expresiones multidimensionales (MDX) válida que devuelve una referencia a un objeto MDX.  
  
 *Expression2*  
 Expresión MDX válida que devuelve una referencia a un objeto MDX.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano que devuelve **true** si ambos argumentos hacen referencia al mismo objeto; en caso contrario, **false**. Si el **NULL** se especifica la palabra clave, el operador devuelve **true** si *Expression1* es **null**; en caso contrario, **false** .  
  
## <a name="remarks"></a>Comentarios  
 El **IS** operador a menudo se usa para determinar si las tuplas y miembros son idempotentes, lo que significa que son exactamente equivalentes.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra cómo usar el **IS** operador para comprobar si el miembro actual en un eje es un miembro específico:  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores de MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
