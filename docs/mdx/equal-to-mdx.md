---
title: = (Igual a) (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 189facb54de244ff220b41ec08c8b02faf5a2c27
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139323"
---
# <a name="-equal-to-mdx"></a>= (Igual a) (MDX)


  Realiza una operación de comparación que determina si el valor de una expresión multidimensional (MDX) es igual al valor de otra expresión MDX.  
  
> [!NOTE]  
>  Para comparar objetos, utilice el operador [IS &#40;MDX&#41;](../mdx/is-mdx.md) . Por ejemplo, use el operador IS cuando compruebe si el miembro actual en un eje de consulta es un miembro en concreto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parámetros  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano basado en las condiciones siguientes:  
  
-   **true** si el valor del primer parámetro es igual al valor del segundo parámetro.  
  
-   **false** si el valor del primer parámetro no es igual al valor del segundo parámetro.  
  
-   **true** si ambos parámetros son NULL o un parámetro es NULL y el otro es 0.  
  
## <a name="examples"></a>Ejemplos  
 La consulta siguiente muestra ejemplos de estas condiciones:  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
