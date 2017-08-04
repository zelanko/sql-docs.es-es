---
title: = (Igual a) (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- =
dev_langs:
- kbMDX
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 5e1f3b58-a646-4fc1-a3f1-19090a5437b7
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9e446cf812f57a3cc3df74728b74c072d1b089bc
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="-equal-to-mdx"></a>= (Igual a) (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una operación de comparación que determina si el valor de una expresión multidimensional (MDX) es igual al valor de otra expresión MDX.  
  
> [!NOTE]  
>  Para comparar objetos, use la [IS &#40; MDX &#41; ](../mdx/is-mdx.md) operador. Por ejemplo, use el operador IS cuando compruebe si el miembro actual en un eje de consulta es un miembro en concreto.  
  
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
 [Referencia de operadores MDX &#40; MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  

