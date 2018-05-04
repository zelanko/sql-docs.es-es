---
title: ES (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IS
dev_langs:
- kbMDX
helpviewer_keywords:
- IS operator
ms.assetid: dc8c0b91-3bb1-49e5-8d70-57545baaa8e0
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a4422a686a35799c210f81d5e60fa44ca3c5aeae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
