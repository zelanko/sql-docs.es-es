---
title: ES (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: IS
dev_langs: kbMDX
helpviewer_keywords: IS operator
ms.assetid: dc8c0b91-3bb1-49e5-8d70-57545baaa8e0
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: db81591072109dd9f83ce2bc69db6bc09fa15e37
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="is-mdx"></a>IS (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>Comentarios  
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
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
