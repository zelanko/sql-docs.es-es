---
title: ES (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5c36a5f45e34d6d78043f6ce8a3e3fb040ecc9f6
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578597"
---
# <a name="is-mdx"></a>IS (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Un valor booleano que devuelve **true** si ambos argumentos hacen referencia al mismo objeto; en caso contrario, **false**. Si el **NULL** se especifica la palabra clave, el operador devuelve **true** si *Expression1* es **null**; en caso contrario, **false**.  
  
## <a name="remarks"></a>Notas  
 El **IS** se suele usar para determinar si tuplas y miembros son idempotentes, lo que significa que son exactamente equivalentes.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo utilizar el **IS** operador para comprobar si el miembro actual en un eje es un miembro específico:  
  
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
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
