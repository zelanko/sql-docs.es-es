---
title: = (Igual a) (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb609b1a3bcfe08d0720aef70e584049080be148
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578177"
---
# <a name="-equal-to-mdx"></a>= (Igual a) (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza una operación de comparación que determina si el valor de una expresión multidimensional (MDX) es igual al valor de otra expresión MDX.  
  
> [!NOTE]  
>  Para comparar objetos, use la [IS &#40;MDX&#41; ](../mdx/is-mdx.md) operador. Por ejemplo, use el operador IS cuando compruebe si el miembro actual en un eje de consulta es un miembro en concreto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>Parámetros  
 *MDX_Expression*  
 Una expresión MDX válida.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor booleano basado en las condiciones siguientes:  
  
-   **True** si el valor del primer parámetro es igual que el valor del segundo parámetro.  
  
-   **false** si el valor del primer parámetro no es igual que el valor del segundo parámetro.  
  
-   **True** si ambos parámetros son null, o un parámetro es null y el otro parámetro es 0.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de operadores MDX &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
