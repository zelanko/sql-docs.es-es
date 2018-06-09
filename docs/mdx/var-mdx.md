---
title: Var (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14caf6e96b41fdf2e7f8b4d20f16852e890bd166
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743924"
---
# <a name="var-mdx"></a>Var (MDX)


  Devuelve la varianza de muestra de una expresión numérica evaluada sobre un conjunto mediante la fórmula de población no sesgada (al dividir por *n*).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Var(Set_Expression [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Numeric_expression*  
 Expresión numérica válida que suele ser una expresión MDX de las coordenadas de celdas que devuelven un número.  
  
## <a name="remarks"></a>Notas  
 El **Var** función devuelve la varianza no sesgada de una expresión numérica especificada evaluada sobre un conjunto especificado.  
  
 El **Var** función utiliza la fórmula de población no sesgada y la [VarP](../mdx/varp-mdx.md) función utiliza la fórmula de población sesgada.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
